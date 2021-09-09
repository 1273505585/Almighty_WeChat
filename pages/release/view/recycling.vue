<template>
  <view class="content">
    <!-- 加载动画 -->
    <orange-fullloading
      text="加载中"
      :loadshow="loadingStatus">
    </orange-fullloading>
	 <view>
		 <u-navbar title="废品回收" :backTextStyle="{color:'#ffffff'}" :background="background"></u-navbar>
     </view>
	 <view >
		 <u-notice-bar type="success" :list="list1" ></u-notice-bar>
		 	<u-toast ref="uToast" />
		  <u-form :model="form" ref="uForm">
			  <u-select v-model="show" :list="list" @confirm="classification"></u-select>
			  <u-select v-model="show1" :list="list2" @confirm="classification"></u-select>
		 	<u-field v-model="form.intro" label-width=50 type="textarea" maxlength=30 placeholder="其他类型的废品,请在这里备注一下哦~"></u-field>
		 	<u-field v-model="form.classification" @click="show=true" label-width=100 :disabled=true icon="grid" label="分类" input-align="right" placeholder="请选择废品类型"></u-field>
			<u-field v-model="form.floor" @click="show1=true" label-width=150 :disabled=true icon="grid" label="宿舍楼" input-align="right" placeholder="请选择宿舍楼"></u-field>
			<u-field v-model="form.dormitory" label-width=100  icon="grid" label="分类" input-align="right" placeholder="请输入宿舍号"></u-field>
		 	<u-field v-model="form.pirce" maxlength=10 label-width=100 :disabled=true icon="rmb" label="价格" input-align="right" ></u-field>
			<u-field v-model="form.qq" maxlength=11 label-width=100 icon="qq-fill" label="QQ" input-align="right" placeholder="输入您的QQ号码,方便联系您" ></u-field>
			<view style="padding: 30px 0px 0px 0px;">
		 	<u-button type="success" shape="circle" :ripple=true  @click="onclick">提交</u-button></view>
		 </u-form>
		
		
	 </view>
  </view>
</template>

<script>
export default {
  data () {
    return {
		background: {
			'background-image': 'linear-gradient(45deg, rgb(28, 187, 180), rgb(141, 198, 63))'
		},
		action: '',//上传服务器地址
		show: false,
		show1:false,
		qq:false,
		cek:false,
		list2:[
			{
				value: 'A1',
				label: 'A1'
			},
			{
				value: 'A2',
				label: 'A2'
			},
			{
				value: 'A3',
				label: 'A3'
			},
			{
				value: 'A4',
				label: 'A4'
			},
			{
				value: 'A5',
				label: 'A5'
			},
			{
				value: 'A6',
				label: 'A6'
			},
			{
				value: 'A7',
				label: 'A7'
			},
			{
				value: 'A8',
				label: 'A8'
			},
			{
				value: 'A9',
				label: 'A9'
			},
			{
				value: 'A10',
				label: 'A10'
			},
			{
				value: 'A11',
				label: 'A11'
			},
			{
				value: 'A12',
				label: 'A12'
			},
			{
				value: '北区',
				label: '北区'
			}
			],
		list1: ["无需出门，上门回收废品哦！"],
		list: [
			{
				value: '安卓',
				label: '安卓'
			},
			{
				value: '苹果',
				label: '苹果'
			}
			],
		form: {
			floor:"",
			dormitory:"",
			title: "",
			intro: "",
			classification: "",
			pirce:"上门回收,面议",
			qq:"",
		},
		
		radio: '',
		switchVal: false,
		title:"跑腿做事",
		value:"",
		options: [{
				label: '商品买卖',
				value: '商品买卖',
			},
			{
				label: '跑腿做事',
				value: '跑腿做事',
			},
			{
				label: '代刷网课',
				value: '代刷网课',
			},
			{
				label: '王者服务',
				value: '王者服务',
			},
			{
				label: '发布兼职',
				value: '发布兼职',
			},
			{
				label: '发布需求',
				value: '发布需求',
			},
			{
				label: '发布出租',
				value: '发布出租',
			}
			],
      nopictures: this.$Management.nopictures,
      tabarIndex: 0,
      scrollInto: '',
      category: [],
      rightMenu: [],
      allRightMenu: [],
      loadingStatus: true
    }
  },
  onLoad () {
    this.loadData()
  },
  methods: {
	  radioGroupChange(detail){
		  
		  if(detail.value){this.qq=true;this.cek=true}else{this.qq=false;this.cek=false}
	  },
	  close(index){
		  if(this.value!=""){this.title=this.value;}
	  },
    async loadData () {
      setTimeout(() => {
        this.loadingStatus = false
      }, 100)
    },  
	 classification(e){
	 	this.form.classification=e[0].label
	 },
	 onclick(){//做对图片的上传表格的判断
	 if(this.form.title==""||this.form.pirce==""||this.form.classification==""||this.form.intro==""){
	 	this.$refs.uToast.show({
	 		title: '喔哦！还有内容没有填呢。',
	 		type:"warning"
	 	})
	 	return;
	 }
	 	console.log(this.form)
	 }
},
}
</script>
<style lang="scss">
  .content {
    height: 100%;
  }
  .page{
  	 background-color: rgb(28, 187, 180);
  }
</style>
