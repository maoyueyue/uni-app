<template>
	<div class="container">
		<h2>任务中心</h2>
		<div class="preview">
			<img :src="imgUrl" />
		</div>
		<form>
			<div class="upload">
				选择文件
				<input type="file" @change="getFile($event)" />
			</div>
			<br />
			<button @click="submit($event)" class="sub-btn"></button>
		</form>
	</div>
</template>

<script>
	export default {
		name:'Task',
		data() {
			return {
				imgUrl:'https://static-cdn-oss.mosoteach.cn/mssvc/icons/icon_cc_cover1@2x.png',
				file:''
			};
		},
		methods: {
			getFile:function(event){
				this.file = event.target.files[0];
				var windowURL = window.URL || window.webkitURL;
				alert(windowURL.createObjectURL(this.file));
				this.imgUrl = windowURL.createObjectURL(this.file);
			},
			submit:function(event){
				event.preventDefault();
				let formData = new FormData();
				formData.append('file',this.file);
				this.$http.post('http://localhost:8080/upload',formData).then(function(response){
					alert(response.data);
					this.imgUrl = response.data;
				});
			}

			
		}
		
	}
</script>
<style scoped>
	
</style>
