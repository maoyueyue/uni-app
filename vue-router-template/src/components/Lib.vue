<template>
	<div class="container">
		<div class="lib-bar">
			<router-link to="/topic_lib">题库</router-link>
			<router-link to="/resource_lib">资源库</router-link>
			<router-link to="/exercise_lib">活动库</router-link>
		</div>
		<div class="lib-content"><router-view /></div>
	</div>
</template>

<script>
export default {
	name: 'Lib',
	data() {
		return {
			
		};
	}
};
</script>

<style scoped>
	.container {
		display: flex;
		width: 90%;
		height: 90%;
		margin: 0 auto;
		flex-direction: column;
	}
	.lib-bar {
		height: 10%;
		display: flex;
		align-items: center;
		background-color: #fff;
		margin-top: 20px;
		padding-left: 30px;
	}
	.lib-content{
		text-align: left;
		background-color: #fff;
		margin-top: 30px;
		height: 80%;
		padding-left: 30px;
	}
</style>
