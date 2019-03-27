<template>
	<!-- 根容器 -->
	<div class="container">
		<router-link to="/new_course"><img src="../assets/plus.png" class="logo" /></router-link>
		<div class="t">
			<input type="text" placeholder="搜索" class="box" />
			<button type="button" class="search">搜索</button>
		</div>
		<div class="top">
			<span class="top-tcard">进行中的班课</span>
			<span class="top-card">{{ courses.length }}门进行中的班课</span>
		</div>

		<img src="../assets/hr.png" class="hrc" />
		<div class="course-conainer">
			<div class="course" v-for="(course, index) in courses" :key="index">
				<div class="course-cover">
					<router-link :to="'/course/' + course.courseId">
						<img :src="course.cover" />
					</router-link>
				</div>
				<div class="course-class">
					<br />
					<span class="title2">{{ course.courseClass }}</span>
					<br />
					<span class="title">{{ course.courseName }}</span>
					<br />
					<div class="bt-card">
						<img class="avatar" :src="course.avatar" />
						<span class="code2" v-if="loginUserId === course.userId">
							{{ course.username }}
						</span>
						<span class="title" v-else="">{{ course.username }}</span>

						<span v-if="loginUserId === course.userId" class="course-code">
							{{ course.courseCode }}
						</span>
					</div>
				</div>
			</div>
		</div>

		<div class="top">
			<span class="top-tcard">结束的班课</span>
			<span class="top-card">{{ finishs.length }}门结束的班课</span>
		</div>

		<div><img src="../assets/hr.png" class="hrc" /></div>
		<div class="course-conainer card">
			<div class="course" v-for="(finish, index1) in finishs" :key="index1">
				<div class="course-cover">
					<router-link :to="'/course/' + finish.courseId">
						<img :src="finish.cover" />
					</router-link>
				</div>
				<div class="course-class">
					<br />
					<span class="title2">{{ finish.courseClass }}</span>
					<br />
					<span class="title">{{ finish.courseName }}</span>
					<br />
					<div class="bt-card">
						<img class="avatar" :src="finish.avatar" />
						<span class="code2" v-if="loginUserId === finish.userId">
							{{ finish.username }}
						</span>
						<span class="title" v-else="">{{ finish.username }}</span>
						<span v-if="loginUserId === finish.userId" class="course-code">
							{{ finish.courseCode }}
						</span>
					</div>
				</div>
			</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'Index',
	data() {
		return {
			loginUserId: 3,
			courses: [],
			finishs: []
		};
	},
	created() {
		var _this = this;
		this.$http.get('http://localhost:8080/api/doing/0').then(function(response) {
			_this.courses = response.data;
		});
		this.$http.get('http://localhost:8080/api/finish/1').then(function(response) {
			_this.finishs = response.data;
		});
	}
};
</script>
<style scoped>
.container {
	padding-right: 30px;
	padding-left: 30px;
	width: 63.6%;
	margin: 0 auto;
	padding-top: 20px;
}
.course-conainer {
	display: flex;
	flex-wrap: wrap;
}
.course {
	width: 225px;
	height: 320px;
	margin-right: 10px;
	margin-left: 10px;
	margin-bottom: 30px;
	background-color: #fff;
	display: flex;
	flex-direction: column;
	padding-bottom: 10px;
	border: #ffffff 5px solid;
}
.course-cover img {
	width: 100%;
	height: 225px;
}
.title {
	font-size: 14px;
	color: #333;
	margin-left: 10px;
}
.title2 {
	font-size: 16px;
	color: #333;
	margin-left: 10px;
}
.btn {
	width: 100px;
	height: 40px;
	border: 1px solid #fff;
	background-color: rgb(0, 187, 221);
	border-radius: 20px;
	outline: none;
	color: #fff;
	font-size: 16px;
	margin-left: 11px;
	margin-bottom: 15px;
	cursor: pointer;
}
.btn:hover {
	background-color: rgb(48, 199, 227);
}

.course-code {
	color: rgb(0, 187, 221);
	margin-left: 75px;
	font-size: 14px;
}
.card {
	-webkit-filter: grayscale(100%);
}
.top {
	height: 20px;
	margin-bottom: 10px;
}
.top-card {
	margin-right: 10px;
	float: right;
	color: #4d4d4d;
}
.top-tcard {
	margin-left: 10px;
	color: black;
	font-size: 14px;
}
.hrc {
	width: 98.2%;
	margin-left: 10px;
	margin-bottom: 10px;
}
.avatar {
	width: 30px;
	height: 30px;
	border-radius: 50%;
	margin-left: 10px;
	margin-top: 5px;
	float: left;
}
.code2 {
	color: rgb(0, 187, 221);
	font-size: 14px;
	margin-left: 10px;
}
.bt-card {
	display: flex;
	width: 100%;
	align-items: center;
	height: 35px;
}
.logo {
	border-radius: 50%;
	width: 40px;
	height: 40px;
	margin-left: 13px;
	margin-top: 10px;
}
.t {
	margin-left: 325px;
	align-items: center;
	height: 35px;
	margin-bottom: 13px;
}

.box {
	width: 400px;
	height: 25px;
	border-radius: 5px;
	border: #00bbdd 1px solid;
	outline: none;
	text-indent: 10px;
}

.search {
	height: 29px;
	width: 50px;
	background-color: #00bbdd;
	color: white;
	border-radius: 5px;
	border: none;
	outline: none;
	outline: none;
}
</style>
