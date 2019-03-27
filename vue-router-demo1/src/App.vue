<template>
	<div id="app">
		<div class="header">
			<router-link to="/">
				<img src="./assets/logo.png" class="logo"/>
			</router-link>
			<img src="./assets/work.png" class="cover2 slogo"/><router-link to="/task" class=" nav-item">任务中心</router-link><span>|</span>
			<img src="./assets/kuk.png" class="slogo"/><router-link to="/lib" class="nav-k nav-item">库管理</router-link><span>|</span>
			<img src="https://public-cdn-oss.mosoteach.cn/avatar/2017/61/d24ec0850b3654911abca0c96997c826.png?v=1505461372&x-oss-process=style/s200x200" class="rad slogo"/><router-link to="/ucenter" class="nav-k nav-item">王小榴</router-link>
		</div>
		<div class="container"><router-view></router-view></div>
	</div>
</template>

<script>
export default {
	name: 'App'
};
</script>

<style >
#app {
	background-color: rgb(244, 244, 244);
}
.header {
	display: flex;
	height: 50px;
	background-color: #fff;
	padding-left: 23.5%;
	align-items: center;

}
.nav-item {
	font-size: 17px;
	margin-left: 10px;
	margin-right: 10px;
	color: #333333;
}
.nav-k {
	width: 55px;
}
span {
	font-size: 14px;
	color: darkgray;
}
.logo{
	widows: 80px;
	height: 30px;
	margin-right: 200px;
}
.container {
	width: 85%;
	margin: 0 auto;
	padding-bottom: 40px;
}
a {
	text-decoration: none;
	color: #aaa;
}
a:hover {
	color: rgb(2,165,218);
}

.slogo {
	width: 30px;
	height: 30px;
	margin-left: 10px;
}
.righeader {
	align-items: center;
}
.rad {
	border-radius: 50%;
}
.cover2 {
	margin-left: 320px;
}

</style>