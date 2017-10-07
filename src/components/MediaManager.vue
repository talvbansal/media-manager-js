<template>
	<div class="media-manager">
		<div class="header">
			<button v-if="isModal" type="button" class="close" @click="close()">×</button>
			<main-tool-bar></main-tool-bar>
		</div>

		<div class="content-body dropzone">
			<div class="breadcrumbs">
				<ol class="breadcrumb">
					<li v-for="(name, key) in breadCrumbs">
						<a href="javascript:void(0);" @click="loadFolder(key)">{{ name }}</a>
					</li>
					<li class="active"> {{ folderName }}</li>
				</ol>
			</div>

			<div v-if="isFolderEmpty" class="content-empty">
				<h4>This folder is empty.</h4>
				<p>
					Drag and drop files onto this window to upload files.
				</p>
			</div>

			<div v-else>
				<div class="table-responsive">
					<table class="table table-condensed">
						<thead>
						<tr>
							<th>Name</th>
							<th>Type</th>
							<th>Date</th>
						</tr>
						</thead>
						<tbody>
						<!-- folders -->
						<tr v-for="folder in folders">
							<td>
								<i class="icon-folder"></i>
								<a href="javascript:void(0);">{{ folder.name }}</a>
							</td>
							<td>folder</td>
							<td>{{ folder.modified_date | moment(dateFormat) }}</td>
						</tr>
						<!-- files -->
						<tr v-for="file in files">
							<td>
								<i class="icon-file-text2"></i>
								<a href="javascript:void(0);">{{ file.name }}</a>
							</td>
							<td>{{ file.mimeType }}</td>
							<td>{{ file.modified_date | moment(dateFormat) }}</td>
						</tr>
						</tbody>
					</table>
				</div>
			</div>

		</div>

		<div class="footer">
			<div class="item-count">
				{{ itemsCount }} Items
			</div>
		</div>
	</div>
</template>

<style>

</style>

<script>
  import MainToolBar from './MainToolBar'
  import Axios from 'axios'

  export default {
    components: {
      MainToolBar
    },

    props: {

      dateFormat: {
        default: 'DD/MM/YYY'
      },

      isModal: {
        default: false
      },

      url: {
        default: () => {
          return {
            load: '/browser/index'
          }
        }
      }
    },

    data () {
      return {
        /**
         * breadCrumbs for the current path that are used to go
         * backwards through the directory tree.
         */
        breadCrumbs: {},

        /**
         * The currently highlighted file
         */
        currentFile: null,

        /**
         * The current path that the media manager is displaying
         */
        currentPath: null,

        /**
         * All of the files in the current path
         */
        files: [],

        /**
         * The current path's folder name
         */
        folderName: null,

        /**
         * All of the sub folders in the current path
         */
        folders: [],

        /**
         * Property to show the loading indicator
         */
        loading: true,

        /**
         * Property to show upload progress
         */
        uploadProgress: 0,

        /**
         * Total files and folder count
         */
        itemsCount: 0

      }
    },

    computed: {
      isFolderEmpty () {
        return ((this.files.length + this.folders.length) === 0)
      }
    },

    mounted () {
      this.loadFolder()
    },

    methods: {
      close () {
        this.breadCrumbs = {}
        this.currentFile = null
        this.currentPath = null
        this.files = {}
        this.folderName = null
        this.folders = {}
        this.itemsCount = 0
      },

      loadFolder (path = '') {
        this.currentFile = false
        this.loading = true

        Axios.get(`${this.url.load}?path=${path}`).then(
          (response) => {
            this.breadCrumbs = response.data.breadCrumbs
            this.currentFile = null
            this.currentPath = response.data.folder
            this.files = response.data.files
            this.folderName = response.data.folderName
            this.folders = response.data.subFolders
            this.itemsCount = response.data.itemsCount
            this.loading = false
          }).catch((error) => {
            if (error.response.data.error) {
              this.mediaManagerNotify(error.response.data.error, 'danger')
            }

            this.loading = false
            this.currentFile = null
          }
        )
      }
    }
  }
</script>
