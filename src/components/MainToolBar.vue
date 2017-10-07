<template>
	<div class="btn-toolbar">
		<div class="btn-group mr-2">
			<label class="btn btn-primary btn-icon-text btn-file">
				<i class="icon-upload"></i>
				<span class="hidden-xs">Upload</span>
			</label>

			<button class="btn btn-primary btn-icon-text" type="button" title="Add Folder">
				<i class="icon-folder-plus"></i>
				<span class="hidden-xs">Add folder</span>
			</button>
		</div>

		<div class="btn-group mr-2">
			<button class="btn btn-default btn-icon-text" type="button" title="Refresh">
				<i class="icon-loop2"></i>
				<span class="hidden-xs">Refresh</span>
			</button>
		</div>

		<div class="btn-group">
			<button class="btn btn-default btn-icon-text" type="button" :disabled="!currentFile" title="Move">
				<i class="icon-arrow-right"></i>
				<span class="hidden-xs">Move</span>
			</button>

			<button class="btn btn-default btn-icon-text" type="button" :disabled="!currentFile" title="Delete">
				<i class="icon-bin"></i>
				<span class="hidden-xs">Delete</span>
			</button>

			<button class="btn btn-default btn-icon-text" type="button" :disabled="!currentFile" title="Rename">
				<i class="icon-pencil"></i>
				<span class="hidden-xs">Rename</span>
			</button>
		</div>

	</div>
</template>

<script>
  export default {
    props: ['currentFile']
  }
</script>
