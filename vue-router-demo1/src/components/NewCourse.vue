<template>
	<div class="container">
		<div class="title"><span>当前位置: 班课列表 > 创建班课</span></div>
		<div class="mess">
			<span>班级</span>
			<span class="xhz">*</span>
		</div>
		<input type="text" placeholder="请填写班级" v-model="course.courseClass" class="input-box" />
		<div class="mess">
			<span>课程</span>
			<span class="xhz">*</span>
		</div>
		<input type="text" placeholder="请填写课程" v-model="course.courseName" class="input-box" />
		<div class="meeage"><input type="checkbox"  /><span>学校班课课表</span><span class="dar">（学校课表班课就是学校安排课程表里的正式班课）</span></div>
		<div class="co">
			<span>设置班课封面</span>
			<div class="preview" @click="handleClick()">
				<img :src="imgUrl" class="cover" v-if="!show" />
				<img src="../assets/and.png" class="icon-plus" v-if="show" />
				<input
					type="file"
					@change="getFile($event)"
					style="display: none;"
					id="coverFile"
				/>
			</div>
		</div>
		<div><button @click="addCourse(course)" class="btn">确定</button><button @click="back" class="backbtn">取消</button></div>
	</div>
</template>

<script>
export default {
	name: 'NewCourse',
	data() {
		return {
			loginUserId: 3,
			file: '',
			show: true,
			course: {
				courseName: '',
				courseClass: '',
				cover:''
			},
			imgUrl:''
		};
	},
	methods: {
		//点击图片预览区，即模拟点击文件选择组件
		handleClick: function() {
			document.getElementById('coverFile').click();
		},
		//图片预览
		getFile: function() {
			this.file = event.target.files[0];
			var windowURL = window.URL || window.webkitURL;
			this.imgUrl = windowURL.createObjectURL(this.file);
			this.show = false;
		},
		addCourse: function(course) {
			course.cover=this.imgUrl;
			var _this = this;
			this.$http({
				method: 'post',
				url: 'http://localhost:8080/api/course',
				data: {
					userId: _this.loginUserId,
					courseName: course.courseName,
					courseClass: course.courseClass,
					cover: course.cover,
					finished: 0
				}
			}).then(function() {
				alert('新增班课成功');
				_this.$router.push('/');
			});
		},
		back:function(){
			var _this = this;
			_this.$router.push('/');
		}

	}
};
</script>
<style scoped>
.container {
	display: flex;
	flex-direction: column;
	width: 62.5%;
	margin: 0 auto;
	background-color: #fff;
	height: 600px;
}
.input-box {
	width: 600px;
	height: 40px;
	border: 1px solid #d6d6d6;
	color: black;
	text-indent: 10px;
	margin-bottom: 20px;
	font-size: 14px;
	margin-top: 10px;
	margin-left: 200px;
}
.btn {
	margin-top: 70px;
	width: 100px;
	height: 40px;
	border: 1px solid rgb(0, 187, 221);
	background-color: #fff;
	outline: none;
	color: rgb(0, 187, 221);
	font-size: 16px;
	cursor: pointer;
	margin-left: 350px;	
}
.backbtn {
	margin-top: 70px;
	width: 100px;
	height: 40px;
	border: 1px solid #333333;
	background-color: #fff;
	outline: none;
	color: #333333;
	font-size: 16px;
	cursor: pointer;
	margin-left: 100px;	
}
.preview {
	margin-top: 10px;
	width: 110px;
	height: 110px;
	border: 2px dashed #aaa;
	cursor: pointer;
	display: flex;
	justify-content: center;
	align-items: center;
}
.co {
	margin-top: 30px;
	margin-left: 200px;
}
.icon-plus {
	width: 70px;
	height: 70px;
}
.cover {
	width: 100%;
	height: 100%;
}
span {
	color: #333333;
}
.title {
	display: flex;
	height: 50px;
	margin-bottom: 70px;
	width: 100%;
	background-color: #f4f4f4;
	align-items: center;
}
.xhz {
	color: red;
}
.mess {
	margin-left: 200px;
}
.dar {
	color: darkgrey;
}
.meeage {
	display: flex;
	justify-content: center;
	margin-right: 185px;
}
</style>
