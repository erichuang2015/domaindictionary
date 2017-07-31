<template>
	<div>
		<router-view class="main-viewport"></router-view>
	</div>
</template>

<script>
	/*
	 * libs
	 */
	import { mapGetters }					from "vuex";


	export default {
		name: "app",
		computed: {
			...mapGetters([
			])
		},
		methods: {
		}
	}
</script>

<style >

	html {
		margin: 0;
		padding: 0;
	}

	body {
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
		font-family: 'Titillium Web', sans-serif;
		color: #8c829b;
		margin: 0;
		padding: 0;
		width: 100%;
		height: 100%;
		background: #221d2a;
		font-size: 18px;
	}

	h1, h2, h3, h4, h5, h6, p, ul, li {
		margin: 0;
		padding: 0;
		font-weight: normal;
		margin-bottom: 16px;
	}

	a {
		color: #9d7660;
		text-decoration: none;
	}

	a:hover{
		color: #82718e;
	}

	span {
		width: 100%;
		float: left;
	}

	h2 {
		margin-bottom: 32px;
		font-size: 22px;
		font-weight: normal;
	}

	.main-viewport {
		float: left;
		padding: 32px;
		width: 100%;
	}


	button, input {
		outline: none;
		background: rgba(85, 85, 96, 0.1);
		border: none;
		padding: 8px;
		font-family: 'Titillium Web', sans-serif;
		font-size: 18px;
		color: #c8c8c8;
		float: left;
		width: calc(100% - 16px);
		margin-bottom: 16px;
	}

	input[type="text"]{
		width: calc(100% - 32px);

	}

	button:hover {
		opacity: 0.8;
		cursor: pointer;
	}

</style>
