<template>
	<view>
		<u-toast ref="uToast" />
		<u-upload ref="uUpload" :action="action" :auto-upload="false" max-count=5></u-upload>
	 <u-form :model="form" ref="uForm">
		<u-field v-model="form.title" label-width=50 maxlength=10 placeholder="描述你的标题"></u-field>
		<u-field v-model="form.intro" label-width=50 type="textarea" maxlength=30 placeholder="描述一下你要卖的宝贝,准确的描述能更快卖出哦~"></u-field>
		<u-select v-model="show" :list="list" @confirm="classification"></u-select>
		<u-field v-model="form.classification" :disabled=true label-width=100 icon="grid" label="分类" input-align="right" placeholder="选择你的分类" @click="show=true"></u-field>
		<u-field v-model="form.pirce" maxlength=5 label-width=100 icon="rmb" label="价格" input-align="right" placeholder="输入商品价格" ></u-field>
		<u-button type="success" shape="circle" :ripple=true @click="onclick">发布</u-button>
	</u-form>
	
	
	</view>
</template>

<script>
export default {
	data() {
		return {
			action: '',//上传服务器地址
			show: false,
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
				pirce:""
			},
			
			radio: '',
			switchVal: false
		};
	},
	methods:{
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
	}
};
</script>
<style>
	.r{bottom:0;}
</style>