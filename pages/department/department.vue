<template>
	<view class="container">
		<headerFrom :menu='menu' @redirectToFrom='redirectToFrom'></headerFrom>
		<view class="segmented d-flex just-content-center">
			<view
				class="segmented-btn d-flex flex-column justify-content-center align-items-center"
				v-for="(item, i) in segmentedItems"
				:key="i"
				@click="onClickItem(i)"
				:class="[current === i ? 'segmented-ative' : '']"
			>
				{{ item }}
			</view>
		</view>
		<view class="content">
			<uni-swiper-dot :current="current" :dots-styles="dotsStyles" mode="dot" field="content" class="h-100">
				<swiper  :current="current" class="swiper-box"  @change="change">
					<swiper-item v-for="(item, index) in info" :key="index" >
						<view :class="item.colorClass" class="swiper-item  h-100">
							<view class="d-flex justify-content-between flex-wrap" >
								<view class="button-item d-flex align-items-center just-content-center" v-for="(child, childIndex) in item" :key="childIndex" @click="navTo(childIndex)">
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
	</view>
</template>

<script>
	import headerFrom from '../../components/header-from.vue'
	export default {
		components:{headerFrom},
		data() {
			return {
				menu:[
					{name:'科室介绍'}
				],
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
					{name:'脾胃科室'},
					{name:'心血管科'},
					{name:'呼吸内科'},
					{name:'消化内科'},
					{name:'神经内科'},
					{name:'儿科'},
					{name:'推拿科'},
					{name:'针灸科'},
					{name:'肿瘤内科'},
					{name:'干部保健科'},
					{name:'睡眠医学科'},
				],
				[
					{name:'普外科'},
					{name:'肛肠科'},
					{name:'骨伤科'},
					{name:'耳鼻喉科'},
					{name:'泌尿科'},
					{name:'空腔科'},
					{name:'男科'},
					{name:'眼科'},
					{name:'皮肤科'},
					{name:'神经外科'},
					{name:'妇科'},
					{name:'妇产科'},
					{name:'医学美容科'},
				],
				[
					{name:'超声科'},
					{name:'医学影像科'},
					{name:'彩超室'},
				]
				],
				segmentedItems: ['内科系统', '外科系统','医技系统'],
			}
		},
		methods: {
			//点击导航栏
			onClickItem(e) {
				if (this.current !== e) {
					this.current = e;
					console.log(this.current);
				}
			},
			//滑动切换
			change(e) {
				if (this.current !== e.detail.current) {
					this.current = e.detail.current;
					console.log(this.current);
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
			//跳转详情
			navTo(index){
				uni.navigateTo({
					url: 'details?name='+this.info[this.current][index].name,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style lang="scss">
	.segmented {
		margin-top: 6px;
		padding: 0rpx 54rpx;
		.segmented-btn {
			font-size: 37px;
			font-weight: bold;;
			color: #fff;
			margin: 0 4px;
			background: #ac937e;
			padding:10px 30px;
			border-radius: 10px;
			box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.345)
		}
		.segmented-ative {
			background-color: rgb(204,153,51);
		}
	}
	.container{
		background-image: url(../../static/img/bg.png) ;
	}
	.content{
		height: 1700px;
	}
	.swiper-box{
		height: 100%;
		margin-top: 40px;
		box-sizing: border-box;
		padding: 100px 120px 0 120px;
		.swiper-item{
			overflow: scroll;
		}
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
