<template>
	<div id="app">
		<link rel="stylesheet" href="https://maxcdn.bootstrapcdn.com/bootstrap/4.0.0-beta/css/bootstrap.min.css" integrity="sha384-/Y6pD6FV/Vv2HJnA6t+vslU6fwYXjCFtcEpHbNJ0lyAFsXTsjBbfaDjzALeQsN6M" crossorigin="anonymous">

		<img src="./assets/logo.png">
		<hello></hello>
		<media-manager></media-manager>
	</div>
</template>

<script>
  import Hello from './components/Hello'
  import MediaManager from './components/MediaManager'

  export default {
    name: 'app',
    components: {
      Hello,
      MediaManager
    }
  }
</script>

<style>
	#app {
		font-family: 'Avenir', Helvetica, Arial, sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		text-align: center;
		color: #2c3e50;
		margin-top: 60px;
	}
</style>
