<template>
	<view class="container">
		<headerFrom :menu='menu' @redirectToFrom='redirectToFrom'></headerFrom>
		<image class="content-img" :src="src" mode="widthFix" @click="previewImages" v-show="src"></image>
		<uni-swiper-dot :info="info" :current="current" :dots-styles="dotsStyles" mode="dot" field="content" class=""  v-show="!src">
			<swiper class="swiper-box" @change="change">
				<swiper-item v-for="(item, index) in info" :key="index" >
					<view :class="item.colorClass" class="swiper-item w-100 h-100">
						<view class="d-flex justify-content-between flex-wrap" >
							<view class="button-item d-flex align-items-center just-content-center" v-for="(child, childIndex) in item" :key="childIndex" @click="navTo(child)">
								<image src="../../static/img/visit-item.png" mode=""></image>
								<view class="d-flex align-items-center just-content-center flex-column button-item-text">
									<text >{{child.name}}</text>
									<text class="explain" v-if="child.explain">{{child.explain}}</text>
								</view>								
							</view>
						</view>
					</view>
				</swiper-item>
			</swiper>
		</uni-swiper-dot>
	
	</view>
</template>

<script>
	import headerFrom from '../../components/header-from.vue'
	export default {
		components:{headerFrom},
		data() {
			return {
				current: 0,
				dotsStyles: {
					backgroundColor: '#C0BFBD',
					border: 'none',
					color: '#fff',
					selectedBackgroundColor: '#fff',
					selectedBorder: 'none',
					bottom: 120,
					width:'50',
					height:'50'
				},
				info:[[
					{name:'就诊流程'},
					{name:'出入院流程'},
					{name:'取药流程'},
					{name:'医保卡',explain:'(使用办法)'},
				]],
				menu:[
					{name:'就诊指导',url:'../visit/visit'}
				],
				src:''
			}
		},
		methods: {
			change(e) {
			    this.current = e.detail.current;
			},
			navTo(data){
				switch(data.name){
					case '就诊流程':
						this.info = [[
							{name:'门诊',explain:'就诊流程'},
							{name:'预约',explain:'就诊流程'},
						]]
						this.menu = [{name:'就诊指导',url:'../visit/visit'},{name:'就诊流程'}]
					    break;
					case '出入院流程':
						this.menu = [{name:'就诊指导',url:'../visit/visit'},{name:'出入院流程'}]
						this.src = '../../static/img/test/visit/admissionProcess.png';
					    break;
					case '取药流程':
						this.menu = [{name:'就诊指导',url:'../visit/visit'},{name:'取药流程'}]
						this.src = '../../static/img/test/visit/medicine-process.png';
					    break;
					case '医保卡':
						this.menu = [{name:'就诊指导',url:'../visit/visit'},{name:'医保卡'}]
						this.src = '../../static/img/test/visit/insurance.png';
					    break;
					case '门诊':
						this.menu = [{name:'就诊指导',url:'../visit/visit'},{name:'就诊流程'}]
						this.src = '../../static/img/test/visit/outpatient-process.png';
					    break;
					case '预约':
						this.menu = [{name:'就诊指导',url:'../visit/visit'},{name:'就诊流程'}]
						this.src = '../../static/img/test/visit/appointment-process.png';
					    break;
				}
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
			//全屏浏览图片
			previewImages(index) {
				let data = [this.src];
				uni.previewImage({
					urls: data
				});
			},
		}
	}
</script>

<style lang="scss">
	.container{
		background-image: url(../../static/img/index/bg.png) ;
	}
	.content-img{
		width: 100%;
	}
	.swiper-box{
		height: 1700px;
		margin-top: 40px;
		width: 100%;
		box-sizing: border-box;
		padding: 230px 120px 0 120px;
		.button-item{
			padding: 37px 0;
			position: relative;
			.button-item-text{
				position: absolute;
				font-size: 53px;
				letter-spacing: 3px;
				font-weight: bold;
				.explain{
					font-size: 45px;
					padding-top: 10px;
				}
			}
			image{
				width: 402px;
				height: 301px;
			}
		}
		
	}
</style>
