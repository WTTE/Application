<template>
	<view>
		<view @click="getNewsDetail">
			<!-- #ifdef MP-WEIXIN -->
			<rich-text :nodes="content"></rich-text>
			<!-- #endif -->
			<!-- #ifdef MP-ALIPAY -->
			<rich-text :nodes="htmlNodes"></rich-text>
			<!-- #endif -->
			<!-- #ifdef H5 -->
			<rich-text :nodes="content"></rich-text>
			<!-- #endif -->
		</view>
	</view>
</template>

<script>
	import { myRequestPost } from "@/utils/zgrequest.js"; 
	import parse from '@/utils/html.js'
	export default {
		data() {
			return {
				content:"" ,
				htmlNodes:[]
			}
		},
		onLoad() {
			this.getNewsDetail( )
		},
		methods: {
			async getNewsDetail(){
				const res = await myRequestPost('/sojourn.equity.custom.web.content',
				{
				"contentNo":"10000001",
				"client":"applets",
				"mobileBrand":"microsoft",
				"mobileModel":"microsoft",
				"osVersion":"Windows 10 x64",
				"timestamp":1607925096000,
				"sign":"8A8410C2566691E44C4007496946B829",
				})
			this.content = res.respData.content
			//#ifdef MP-ALIPAY
			this.htmlNodes = parse(this.content)
			// #endif
			}
		} 
	}
</script>

<style>

</style>
