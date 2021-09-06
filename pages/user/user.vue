<template>
	<view class="page">
		<u-navbar title="我的" :is-back="false" :background="background" titleColor="#fff"></u-navbar>
		<view class="u-flex user-box u-p-30">
			<view class="u-m-r-10" @click="tourl('/pages/login/login')">
				<u-avatar src="/static/pic.jpg" size="140"></u-avatar>
			</view>
			<view class="u-flex-1" @click="tourl('/pages/login/login')">
				<view class="u-font-18 u-p-b-20">{{userinfo.nickName || '点击登录'}}</view>
				<view v-show="userinfo.gender"><u-icon :name="userinfo.gender == 1? 'man':'woman'" color="#6BC362" size="38"></u-icon></view>
			</view>
			<view class="u-m-l-10 u-p-10">
				<u-icon name="scan" color="#969799" size="28" @click="scan"></u-icon>
			</view>
			<view class="u-m-l-10 u-p-10" @click="tourl('/pages/mine/setting',true)">
				<u-icon name="arrow-right" color="#969799" size="28"></u-icon>
			</view>
		</view>
		
		<view class="u-m-t-20">
			<u-cell-group>
				<u-cell-item icon="bag" title="我的订单" :iconStyle="iconStyle" ></u-cell-item>
				<u-cell-item icon="plus" title="我的发布" :iconStyle="iconStyle" ></u-cell-item>
				<u-cell-item icon="bell" title="消息" :iconStyle="iconStyle" ></u-cell-item>
				
				<u-cell-item icon="heart" title="收藏" :iconStyle="iconStyle" ></u-cell-item>		
				<u-cell-item icon="fingerprint" title="足迹" :iconStyle="iconStyle" ></u-cell-item>
				<!-- #ifdef MP-WEIXIN -->
				<button open-type="contact" class="button">
				<u-cell-item icon="server-fill" title="客服" :iconStyle="iconStyle"></u-cell-item>
				</button>
				<!-- #endif -->
				
			</u-cell-group>
		</view>
		
		<view class="u-m-t-20">
			<u-cell-group>
				<u-cell-item icon="setting" title="设置" :iconStyle="iconStyle" @click="tourl('/pages/mine/setting',true)"></u-cell-item>
			</u-cell-group>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				background: {
					'background-image': 'linear-gradient(45deg, rgb(28, 187, 180), rgb(141, 198, 63))'
				},
				show:true,
				iconStyle:{
					'color':'#6BC362'
				},
				userinfo:{}
			}
		},
		onLoad() {
			
		},
		onShow() {

		},
		methods: {
			scan(){	// 扫码 h5不支持
				uni.scanCode({
				    success: function (res) {
				        console.log('条码类型：' + res.scanType);
				        console.log('条码内容：' + res.result);
				    }
				});
			},
			tourl(url){
				this.$common.navigateTo(url)
			},
		}
	}
</script>

<style lang="scss">
page{
	background-color: #ededed;
}

.user-box{
	background-color: #fff;
}
.button{
	border: none;
	background-color: transparent;
	outline: none;
	padding: 0;
}
.button::after{
	outline: none;
	border: none;
}
</style>
