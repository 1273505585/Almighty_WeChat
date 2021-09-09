<template>
	<view class="login">
		模拟登陆
		<br>
		<br>
		<u-input type="text" placeholder="账号" v-model="username"></u-input>
		<u-input type="text" placeholder="密码" v-model="password"></u-input>
		<u-input type="text" placeholder="验证码" v-model="codea"></u-input>
	        <view class="login-code" @click="code">
	          <img :src="codeUrl" class="login-code-img" />
	        </view >
				<br>
				<br>
				<button @click="test">登陆</button>
				<button @click="testa">调用数据</button>
				<button @click="romove">删除token</button>
			</view>	
			
</template>

<script>
	export default {
		data(){
			return{
				username:"",
				password:"",
				codeUrl:"",
				codea:"",
				uuid:""
			}
		},
		mounted() {
        this.code()
		}
		,
		methods:{
			code(){
				this.$R.get('captchaImage').then(res => {
					this.codeUrl = "data:image/gif;base64," + res.img;
					this.uuid = res.uuid;
				});
			},
        test(){   
	
			  
       },
	   testa(){
		   
		   this.$R.get('almighty/user/list1',{code:123},this.token.header).then(res => {
		   console.log(res)
		   });
	   },
	   romove(){
		   uni.removeStorage({
		       key: 'token',
		      
		   });
		   console.log(uni.getStorageSync('token'))
	   }
		},
		}
</script>
<style>
	.login-code {
	  width: 33%;
	  height: 38px;
	  float: right;
	  img {
	    cursor: pointer;
	    vertical-align: middle;
	  }
	  }
	
	.login-code-img {
	  height: 38px;
	}
	.login {
		height: 100%;
		width: 100%;
	   background-image: url('~@/static/common/img/login.jpg');	
	}
</style>