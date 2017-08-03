<template>
	<div class="fixed-top-left">
		<div class="triangle"></div>
		<div class="cube-image">
			<img src="../assets/cube.png">
		</div>
	</div>
</template>

<script>

	export default {

	}
</script>

<style >

	.fixed-top-left {
		position: absolute;
	}

	.cube-image {
		top: 11px;
		left: 11px;
		transform: rotate(-20deg);
		position: absolute;

	}

	.triangle {
		width: 0;
	  height: 0;
		top: -120px;
	  border-top: 120px solid transparent;
	  border-bottom: 120px solid transparent;
	  border-left: 120px solid rgba(255,255,255,0.04);
		position: absolute;
	}

</style>
