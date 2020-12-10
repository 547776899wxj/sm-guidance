<template>
	<view class="container">
		<headerFrom :menu='menu' @redirectToFrom='redirectToFrom'></headerFrom>
		<image class="content-img" :src="src" mode="widthFix" @click="previewImages" v-show="src"></image>
	</view>
</template>

<script>
	import headerFrom from '../../components/header-from.vue'
	export default {
		components:{headerFrom},		
		data() {
			return {
				menu:[
				
				],
				src:''
			};
		},
		onLoad() {
			let data = uni.getStorageSync('temData')||'';
			if(data){
				this.menu = data.menu;
				this.src = data.src;
			}else{
				uni.navigateBack({
					
				})
			}
		},
		methods:{
			//全屏浏览图片
			previewImages(index) {
				let data = [this.src];
				uni.previewImage({
					urls: data
				});
			},
			//导航栏跳转
			redirectToFrom(url){
				uni.redirectTo({
					url: url,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
		}
	}
</script>

<style lang="scss">
	.container{
		background-image: url(../../static/img/bg-noframe.png) ;
	}
	.content-img{
		width: 100%;
	}
</style>
