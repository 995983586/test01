<template>
	<view >
	<input class="shurukuang" type="text" focus="true"  v-model="user" placeholder="请输入用户名" />
	<input class="shurukuang" type="text" focus="true"  v-model="pwd" placeholder="请输入密码"/>	
	<button class="denglu" @click="denglu">登录</button>
	</view>
</template>
<script>
	export default {
		data() {
			return {
				res:"",
				user:"",
				pwd:""
			}
		},
		methods: {	
			denglu:function() {
				var that=this;
				uni.request(
				{
					url:'http://192.168.1.143:8080/Users/login',
					method:'POST',
					header: {
						'content-type': 'application/x-www-form-urlencoded', 
					},				
					data:{userName:that.user,passWord:that.pwd},
					success:function(res){
						console.log(res);
						
						uni.setStorage({
						    key: 'storage_userCode',
						    data: res.data.userCode,
						    success: function () {
						        console.log('success');
						    }
						});
						
						
						if(res.data=="yonghubucunzai"){
							uni.showModal({title:"不存在！"})
						}else{
							if(res.data=="mimacuowu"){
								uni.showModal({title:"密码错误！"})
							}
							else{
								uni.switchTab({
									url:'../index/index'
								})
							}
						}
						}
					}
				
				)
				// uni.clearStorage();
				uni.setStorage({
				    key: 'storage_name',
				    data: that.user,
				    success: function () {
				        console.log('success');
				    }
				});
				uni.setStorage({
				    key: 'storage_psw',
				    data: that.pwd,
				    success: function () {
				        console.log('success');
				    }
				});
			}
	}
	}
</script>
<style>
	.shurukuang{
		margin: 10upx;
		height: 80upx;
		width: 60%;
		/* justify-content:center; */
		align-items: center;
		border: #007AFF 2rpx solid;
		
		margin: 20upx;
		border-radius: 10upx;
		margin-left: 150upx;
	}
	.denglu{
		width: 60%;
	}
</style>
