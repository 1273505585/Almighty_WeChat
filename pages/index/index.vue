<template >
	<view>
		<view class="page">
		<orange-fullloading
		  text="加载中"
		  :loadshow="true">
		</orange-fullloading>
		<view>
			<u-toast ref="uToast" />
			<u-navbar height=44 backIconName="chat" :backTextStyle="{color:'#ffffff'}" :click="chat"  :background="background" titleColor="#fff">
			<u-search placeholder="请输入关键词" :clearabled="true" :animation="true" :clear="clear" v-model="keyword" @custom="TO" @search="TO" ></u-search>
		    </u-navbar>
			<fy-dropdown :menuList="menuList" >
		        <fy-dropdown-item v-model="synthesisValue"  dropdownKey="synthesis"  :options="columnOptions"  @change="handlerColumnChange"></fy-dropdown-item>
		        <fy-dropdown-item v-model="priceValue" dropdownKey="classification" :options="classificationOptions" @change="handlerTypeChange"></fy-dropdown-item>
		        <fy-dropdown-item v-model="salesValue" dropdownKey="arrangement" :options="arrangementOptions" @change="handlerarrangementChange"></fy-dropdown-item>
		    </fy-dropdown>
		</view>
		</view>	
		<view style="padding:88px 0px 0px 0px;">
			
	<view v-for="(items,index) in list" >
	<u-card :title="title" :subTitle="subTitle" :border="false" :index="items.id" :thumb-circle=true sub-title-color="#ff0000" sub-title-size="35" @click="test" style="background-color: #afafaf;" margin="10rpx 10rpx">
		<view class="" slot="body">
			<view class="u-body-item u-flex u-border-bottom u-col-between u-p-t-0">
				<image src="https://img11.360buyimg.com/n7/jfs/t1/94448/29/2734/524808/5dd4cc16E990dfb6b/59c256f85a8c3757.jpg" mode="aspectFill"></image>
				<view class="u-body-item-title u-line-2">{{items.title}}<br>
				</view>
			</view>
		</view>
	</u-card>
	</view>
	</view>
	<u-divider>没有更多了</u-divider>
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
			classificationOptions: [{ label: '筛选条件1', value: 1 }, { label: '筛选条件2', value: 2 }, { label: '筛选条件3', value: 3 }, { label: '筛选条件3', value: 3 }, { label: '筛选条件3', value: 3 }],
			salesValue: '',
			arrangementOptions: [{ label: '筛选条件3', value: 1 }, { label: '筛选条件33', value: 2 }, { label: '筛选条件333', value: 3 }],
			title:"商品买卖",
			subTitle: '¥20',
			keyword:"",
			list:[{
				id:1,
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			},
			{
				id:2,
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			},{
				id:3,
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			},{
				id:4,
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			},{
				id:5,
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			},{
				id:6,
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			},{
				id:7,
				title: '素胚勾勒出青花，笔锋浓转淡',
				subTitle: '2020-05-15',
				thumb: 'http://pic2.sc.chinaz.com/Files/pic/pic9/202002/hpic2119_s.jpg',
			},]

		};
	},
	methods:{
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
		clear(){
			this.keyword=""
		},
		test(index){
			console.log(index)
		},
	}
};
</script>

<style scoped lang="scss">
	.u-card-wrap { 
		background-color: $u-bg-color;
		padding: 1px;
	}
	
	.u-body-item {
		font-size: 32rpx;
		color: #333;
		
	}
		
	.u-body-item image {
		width: 120rpx;
		flex: 0 0 120rpx;
		height: 120rpx;
		border-radius: 8rpx;
		margin-left: 12rpx;
	}
	.page{
		 background-color: #ffffff;
		 width: 100%;
		 position: fixed;
		 _position: static;
		 top: 0px;
		 z-index: 99999;
		 height: 88px;
		 line-height: 36px;
		 _height: 36px;
	}
</style>