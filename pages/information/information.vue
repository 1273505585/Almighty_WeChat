<template>
<view>
	 会话管理
	</view>
	
	    
	
</template>

<script>
	export default {
	    data() {
	        return {
				}
	    },
	    methods: {
	        handlerColumnChange(e) {
				this.menuList[0].title=e
				
	        },
	        handlerTypeChange(e) {
	            this.menuList[1].title=e
	        },
			handlerarrangementChange(e) {
			    this.menuList[2].title=e
			},
	    }
	}
</script>

<style>
	
</style>
