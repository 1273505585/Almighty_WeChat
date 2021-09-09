<template>
  <view class="content">
    <!-- 加载动画 -->
    <orange-fullloading
      text="加载中"
      :loadshow="loadingStatus">
    </orange-fullloading>
	 <view  class="page">
		 <u-navbar title="跑腿做事" :backTextStyle="{color:'#ffffff'}" :background="background"></u-navbar>
     </view>
	 <view >
		 <u-notice-bar type="success" :list="list1" ></u-notice-bar>
		 	<u-toast ref="uToast" />
		 	<u-upload ref="uUpload" :action="action" :auto-upload="false" max-count=5></u-upload>
		  <u-form :model="form" ref="uForm">
		 	<u-field v-model="form.intro" label-width=50 type="textarea" maxlength=30 placeholder="描述一下跑腿的内容,可以是帮拿快递,帮打饭,帮买东西,帮拿外卖等,送货上宿舍!"></u-field>
		 	<u-select v-model="show" :list="list" @confirm="classification"></u-select>
		 	<u-field v-model="form.classification" :disabled=true label-width=100 icon="grid" label="分类" input-align="right" placeholder="选择跑腿类型" @click="show=true"></u-field>
		 	<u-field v-model="form.pirce" maxlength=5 label-width=100 icon="rmb" label="价格" input-align="right" placeholder="输入你给予的佣金" ></u-field>
			<u-field v-model="form.qq" maxlength=11 label-width=100 icon="phone" label="电话" input-align="right" placeholder="输入电话号码" ></u-field>
	
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
		qq:false,
		cek:false,
		list1: ["跑腿只限校园内以及周边，只要您需要，随叫随到！"
						],
		list: [
			{
				value: '1',
				label: '江'
			},
			{
				value: '2',
				label: '湖'
			}
			],
		list2: [
			{
				text:"男"
			},
			{
				text:"女"
			}
						],
		form: {
			title: "",
			intro: "",
			classification: "",
			pirce:"",
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
