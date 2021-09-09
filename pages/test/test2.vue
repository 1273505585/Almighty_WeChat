<template>
	<view class="wrap">
		<view>
			
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
				<view class="demo-warter" v-for="(item, index) in leftList" :key="index">
					<!-- 警告：微信小程序中需要hx2.8.11版本才支持在template中结合其他组件，比如下方的lazy-load组件 -->
					<u-lazy-load threshold="-450" border-radius="10" :image="item.image" :index="index"></u-lazy-load>
					<view class="demo-title">
						{{item.title}}
					</view>
					<view class="demo-price">
						￥{{item.price}}
					</view>
				
					<view class="demo-shop">
						{{item.shop}}
					</view>
					<u-icon name="close-circle-fill" color="#fa3534" size="34" class="u-close" @click="remove(item.id)"></u-icon>
				</view>
			</template>
			<template v-slot:right="{rightList}">
				<view class="demo-warter" v-for="(item, index) in rightList" :key="index">
					<u-lazy-load threshold="-450" border-radius="10" :image="item.image" :index="index"></u-lazy-load>
					<view class="demo-title">
						{{item.title}}
					</view>
					<view class="demo-price">
						￥{{item.price}}
					</view>
					
					<view class="demo-shop">
						{{item.shop}}
					</view>
					<u-icon name="close-circle-fill" color="#fa3534" size="34" class="u-close" @click="remove(item.id)"></u-icon>
				</view>
			</template>
		</u-waterfall>
		<u-loadmore bg-color="rgb(240, 240, 240)" :status="loadStatus" @loadmore="addRandomData"></u-loadmore>
	</view>
</template>

<script>
	export default {
		data() {
			return {
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
				subTitle: '¥20',
				keyword:"",

				loadStatus: 'loadmore',
				flowList: [],
				list: [
					{
						price: 35,
						title: '北国风光，千里冰封，万里雪飘',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic.sc.chinaz.com/Files/pic/pic9/202002/zzpic23327_s.jpg',
					},
					{
						price: 75,
						title: '望长城内外，惟余莽莽',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic.sc.chinaz.com/Files/pic/pic9/202002/zzpic23325_s.jpg',
					},
					{
						price: 385,
						title: '大河上下，顿失滔滔',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
					},
					{
						price: 784,
						title: '欲与天公试比高',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/zzpic23369_s.jpg',
					},
					{
						price: 7891,
						title: '须晴日，看红装素裹，分外妖娆',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2130_s.jpg',
					},
					{
						price: 2341,
						shop: '李白杜甫白居易旗舰店',
						title: '江山如此多娇，引无数英雄竞折腰',
						image: 'http://pic1.sc.chinaz.com/Files/pic/pic9/202002/zzpic23346_s.jpg',
					},
					{
						price: 661,
						shop: '李白杜甫白居易旗舰店',
						title: '惜秦皇汉武，略输文采',
						image: 'http://pic1.sc.chinaz.com/Files/pic/pic9/202002/zzpic23344_s.jpg',
					},
					{
						price: 1654,
						title: '唐宗宋祖，稍逊风骚',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic1.sc.chinaz.com/Files/pic/pic9/202002/zzpic23343_s.jpg',
					},
					{
						price: 1678,
						title: '一代天骄，成吉思汗',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic1.sc.chinaz.com/Files/pic/pic9/202002/zzpic23343_s.jpg',
					},
					{
						price: 924,
						title: '只识弯弓射大雕',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic1.sc.chinaz.com/Files/pic/pic9/202002/zzpic23343_s.jpg',
					},
					{
						price: 8243,
						title: '俱往矣，数风流人物，还看今朝',
						shop: '李白杜甫白居易旗舰店',
						image: 'http://pic1.sc.chinaz.com/Files/pic/pic9/202002/zzpic23343_s.jpg',
					},
				]
			}
		},
		onLoad() {
			this.addRandomData();
		},
		onReachBottom() {
			this.loadStatus = 'loading';
			// 模拟数据加载
			setTimeout(() => {
				this.addRandomData();
				this.loadStatus = 'loadmore';
			}, 1000)
		},
		methods: {
			onPullDownRefresh() {  //下拉刷新时触发的条件
						console.log('触发下拉刷新');
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
			test(index){   
				console.log(index)
			},
			message(){//跳转到会话界面
			 this.$R.get('captchaImage',{username:"admin",password:"123456"}).then(res => {
					console.log(res);
				});
						return;
				this.$u.route({
				url: 'pages/information/information',		
				})
			},
			addRandomData() {
				for(let i = 0; i < 10; i++) {
					let index = this.$u.random(0, this.list.length - 1);
					// 先转成字符串再转成对象，避免数组对象引用导致数据混乱
					let item = JSON.parse(JSON.stringify(this.list[index]))
					item.id = this.$u.guid();
					this.flowList.push(item);
				}
			},
			remove(id) {
				this.$refs.uWaterfall.remove(id);
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