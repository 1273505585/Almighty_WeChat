<template>
	<view>
		<u-navbar back-text="首页" backIconName=" " :backTextStyle="{color:'#ffffff'}"  :background="background" titleColor="#fff">
			<view class="search-wrap" @click="toSearch">
				<u-search height="56" inputAlign="center" placeholder="请输入关键词搜索" :searchIconStyle="searchIconStyle" :showAction="false"></u-search>
			</view>
		</u-navbar>
		<view style="padding:100px 0px 0px 0px;">
			<router-link to="../release/view/second-hand">radio</router-link>
			<router-view name="second-hand"></router-view>
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
				searchIconStyle: {
					'display': 'none'
				},
				swiperList: [
					{image:'/static/banner1.jpg'},
					{image:'/static/banner2.jpg'},
					{image:'/static/banner3.jpg'},
				],
				flowList: [],
				page: 1,
				is_loading: true,
				scrollTop: 0,
				icon: 'arrow-up',
				iconStyle: {
					color: '#ffffff',
					fontSize: '30rpx'
				},
				tips: '顶部',
				customStyle: {
					backgroundColor: '#6BC362',
					color: '#ffffff'
				},
				list:[
					{image:'/static/pic1.jpg'},
					{image:'/static/pic2.jpg'},
					{image:'/static/pic3.jpg'},
					{image:'/static/pic4.jpg'},
				],
				hotimg: '/static/pic2.jpg',
				newimg: '/static/pic4.jpg',
				categoryimg: '/static/pic3.jpg'
			}
		},
		methods: {
			
		}
	};
</script>
<style>
	.search-wrap {
		margin: 0 30rpx 0 10rpx;
		flex: 1;
	}
</style>