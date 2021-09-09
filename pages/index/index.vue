<template>
	<view class="page" v-if="datashow">
		<view>
			<u-loading mode="flower" v-show="show"></u-loading>
			<scroll-view enable-flex="true"> </scroll-view>
			<u-toast ref="uToast" />
			<u-navbar :custom-back="message"  backIconName="chat" :backTextStyle="{color:'#ffffff'}" @click="chat"  :background="background" titleColor="#fff">
			<u-search placeholder="请输入关键词" :clearabled="true" :animation="true" :clear="clear" v-model="keyword" @custom="TO" @search="TO" ></u-search>
		    </u-navbar>
			<u-sticky>
			<fy-dropdown :menuList="menuList" >
		        <fy-dropdown-item v-model="synthesisValue"  dropdownKey="synthesis"  :options="columnOptions"  @change="handlerColumnChange"></fy-dropdown-item>
		        <fy-dropdown-item v-model="priceValue" dropdownKey="classification" :options="classificationOptions" @change="handlerTypeChange"></fy-dropdown-item>
		        <fy-dropdown-item v-model="salesValue" dropdownKey="arrangement" :options="arrangementOptions" @change="handlerarrangementChange"></fy-dropdown-item>
		    </fy-dropdown>
			 </u-sticky>
		</view>
		<u-waterfall v-model="flowList" ref="uWaterfall">
			<template v-slot:left="{leftList}">
				<view class="demo-warter" v-for="(item, index) in leftList" :key="index" @click="test(item.goodsId)">
					<!-- 警告：微信小程序中需要hx2.8.11版本才支持在template中结合其他组件，比如下方的lazy-load组件 -->
					<u-lazy-load threshold="-450" border-radius="10" :image="item.gImageOne" :index="index"></u-lazy-load>
					<view class="demo-title">
						{{item.gTitle}}
					</view>
					<view class="demo-price">
						￥{{item.gPrice}}
					</view>
				
					<view class="demo-shop">
						{{item.uId}}
					</view>
		
				</view>
			</template>
			<template v-slot:right="{rightList}">
				<view class="demo-warter" v-for="(item, index) in rightList" :key="index" @click="test(item.goodsId)">
					<u-lazy-load threshold="-450" border-radius="10" :image="item.gImageOne" :index="index"></u-lazy-load>
					<view class="demo-title">
						{{item.gTitle}}
					</view>
					<view class="demo-price">
						￥{{item.gPrice}}
					</view>
					
					<view class="demo-shop">
						{{item.uId}}
					</view>
					
				</view>
			</template>
		</u-waterfall>
		<u-loadmore bg-color="rgb(240, 240, 240)"  :load-text="loadText" :status="loadStatus" @loadmore="addRandomData"></u-loadmore>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				show:true,
				datashow:false,
				background: {
					'background-image': 'linear-gradient(45deg, rgb(28, 187, 180), rgb(141, 198, 63))'
				},
				menuList: [{ title: '商品买卖', dropdownKey: 'synthesis' }, { title: '分类', dropdownKey: 'classification' }, { title: '排列', dropdownKey: 'arrangement' }],
				synthesisValue: '',
				columnOptions: [{ label: '商品买卖', value: '商品买卖' }, { label: '跑腿做事', value: '跑腿做事' }, { label: '代刷网课', value: '代刷网课' }, { label: '王者服务', value: '王者服务' }, { label: '找兼职', value: '找兼职' }, { label: '找需求', value: '找需求' }, { label: '找出租', value: '找出租' }],
				priceValue: '',
				classificationOptions: [{ label: '筛选条件1', value: 1 }],
				salesValue: '',
				arrangementOptions: [{ label: '价格由高到低', value: 1 }, { label: '价格由低到高', value: 2 }, { label: '最新时间', value: 3 }],
				title:"商品买卖",
				keyword:"",
	            loadText: {
					loadmore: '轻轻上拉',
					loading: '努力加载中',
					nomore: '实在没有了'
				},
				loadStatus: 'loadmore',
				flowList: [],
				list: [
					
				]
			}
		},
		created() {   //加载数据
			this.gdata();
			
		},
		onReachBottom() {
			this.loadStatus = 'loading';
			// 模拟数据加载
			setTimeout(() => {
				this.addRandomData();
				this.loadStatus = 'nomore';
			}, 1000)
		},
		methods: {
			onPullDownRefresh() {  //下拉刷新时触发的条件
						console.log('触发下拉刷新');
						this.addRandomData()
							uni.stopPullDownRefresh();
						
					},
			handlerTypeChange(){
				
			},
			handlerarrangementChange(){
				
			},
			chat(){
				console.log("123")
			},
			handlerColumnChange(){ //第一个选项发生改变触发
				if(this.synthesisValue=="商品买卖"){
					this.menuList[0].title="商品买卖"
				}
				if(this.synthesisValue=="跑腿做事"){
					this.$refs.uToast.show({
						title: '前往APP使用此功能',
						type:"warning"
					})
					return;
				}
				if(this.synthesisValue=="代刷网课"){
					this.$refs.uToast.show({
						title: '前往APP使用此功能',
						type:"warning"
					})
					return;
				}
				if(this.synthesisValue=="王者服务"){
					this.$refs.uToast.show({
						title: '前往APP使用此功能',
						type:"warning"
					})
					return;
				}
				if(this.synthesisValue=="找兼职"){
					this.menuList[0].title="找兼职"
				}
				if(this.synthesisValue=="找需求"){
					this.menuList[0].title="找需求"
				}
				if(this.synthesisValue=="找出租"){
					this.menuList[0].title="找出租"
				}
			},
			TO(){
				console.log("123")
			},
			clear(){ //清除输入框
				this.keyword=""
			},
			test(idx){   
				console.log(idx)
			},
			message(){//跳转到会话界面
	
				this.$u.route({
				url: 'pages/information/information',		
				})
			},
			gdata(){//获取商品的信息
			this.$R.get("almighty/goods/list",{},this.token.header).then(res => {
			    if(res.code!=200){
			    	return uni.showToast({
			    		title: res.msg,
			    		icon: 'none'
			    	})
			    }
				console.log("我能执行到这")
				for(let i=0;i<res.rows.length;i++){
					this.list.push(res.rows[i])
				}
				this.addRandomData();
				this.show=false;
				this.datashow=true;
			});
			},
			addRandomData() {
				this.flowList=[]
				for(let i = 0; i < this.list.length; i++) {
					let index = this.$u.random(0, this.list.length - 1);
					// 先转成字符串再转成对象，避免数组对象引用导致数据混乱
					let item = JSON.parse(JSON.stringify(this.list[index]))
					item.id = this.list[index].id;
					this.flowList.push(item);
					
				}
				
			},
		}
	}
</script>

<style>
	/* page不能写带scope的style标签中，否则无效 */
	page {
		background-color: rgb(240, 240, 240);
	}
</style>

<style lang="scss" scoped>
	.demo-warter {
		border-radius: 8px;
		margin: 5px;
		background-color: #ffffff;
		padding: 8px;
		position: relative;
	}
	
	.u-close {
		position: absolute;
		top: 32rpx;
		right: 32rpx;
	}
	
	.demo-image {
		width: 100%;
		border-radius: 4px;
	}
	
	.demo-title {
		font-size: 30rpx;
		margin-top: 5px;
		color: $u-main-color;
	}
	
	.demo-tag {
		display: flex;
		margin-top: 5px;
	}
	
	.demo-tag-owner {
		background-color: $u-type-error;
		color: #FFFFFF;
		display: flex;
		align-items: center;
		padding: 4rpx 14rpx;
		border-radius: 50rpx;
		font-size: 20rpx;
		line-height: 1;
	}
	
	.demo-tag-text {
		border: 1px solid $u-type-primary;
		color: $u-type-primary;
		margin-left: 10px;
		border-radius: 50rpx;
		line-height: 1;
		padding: 4rpx 14rpx;
		display: flex;
		align-items: center;
		border-radius: 50rpx;
		font-size: 20rpx;
	}
	
	.demo-price {
		font-size: 30rpx;
		color: $u-type-error;
		margin-top: 5px;
	}
	
	.demo-shop {
		font-size: 22rpx;
		color: $u-tips-color;
		margin-top: 5px;
	}
</style>