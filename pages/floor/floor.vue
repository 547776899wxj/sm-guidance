<template>
	<view class="container">
		<headerFrom :menu='menu' @redirectToFrom='redirectToFrom'></headerFrom>
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
					{name:'1号楼',explain:'(门诊楼)'},
					{name:'2号楼',explain:'(急诊楼)'},
					{name:'3号楼',explain:'(医技楼)'},
					{name:'4号楼',explain:'(住院楼)'},
					{name:'5号楼',explain:'(行政楼)'},
				]],
				menu:[
					{name:'楼层指引',url:'../floor/floor'}
				],
			}
		},
		methods: {
			change(e) {
			    this.current = e.detail.current;
			},
			navTo(data){
				uni.setStorageSync('floorName',data.name);
				uni.navigateTo({
					url: 'floorDetails',
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
