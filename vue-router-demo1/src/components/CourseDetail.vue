<template>
	<div class="container">
		<h2>班课{{ id }}详情页面</h2>
		<img :src="course.cover" />
		<p>{{ course.courseName }}</p>
		<p>{{ course.courseClass }}</p>
		<div v-if="course.finished === 0 && loginUserId === course.userId">
			<button @click="finishCourse(course)" class="btn">结束班课</button>
		</div>
		<div v-if="course.finished === 1 && loginUserId === course.userId">
			<button @click="deleteCourse(course.courseId)" class="delbtn">删除班课</button>
		</div>
	</div>
</template>

<script>
export default {
	name: 'CourseDetail',
	data() {
		return {
			id: this.$route.params.id,
			loginUserId: 3,
			course: {}
		};
	},
	methods: {
		finishCourse: function(course) {
			var _this = this;
			this.$http.get('http://localhost:8080/api/course/' + this.id).then(function(response) {
				_this.course = response.data;
			});
			this.$http({
				method: 'put',
				url: 'http://localhost:8080/api/course',
				data: {
					courseId: _this.course.courseId,
					userId: _this.course.userId,
					courseName: _this.course.courseName,
					courseClass: _this.course.courseClass,
					cover: _this.course.cover,
					courseCode: _this.course.courseCode,
					finished: 1
				}
			}).then(function() {
				_this.$router.push('/');
			});
		},
		deleteCourse: function(courseId) {
			var _this = this;
			this.$http({
				method: 'delete',
				url: 'http://localhost:8080/api/course/' + courseId
			}).then(function() {
				alert('班课删除成功');
				_this.$router.push('/');
			});
		}
	},
	created() {
		var _this = this;
		this.$http.get('http://localhost:8080/api/course/' + this.id).then(function(response) {
			_this.course = response.data;
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
.btn {
	width: 100px;
	height: 35px;
	border-radius: 10px;
	background-color: transparent;
	border: 1px #ff0000 solid;
	color: #ff0000;
	cursor: pointer;
	outline: none;
}
.btn:hover {
	border-color: crimson;
	color: crimson;
}
.delbtn {
	width: 100px;
	height: 35px;
	border-radius: 10px;
	background-color: transparent;
	border: 1px darkgray solid;
	color: darkgray;
	cursor: pointer;
}
.delbtn:hover {
	border-color: black;
	color: black;
	outline: none;
}
</style>
