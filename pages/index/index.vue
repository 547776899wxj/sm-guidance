<template>
	<view class="container">
		<view class="top d-flex justify-content-between align-items-center">
			<image class="logo" src="../../static/img/logo.png" mode=""  ></image>
			<view class="position-relative d-flex  just-content-center" >
				<image class="top-icon" src="../../static/img/index/icon.png" mode="" @click="showChooseTemp"></image>
				<view class="choose-temp d-flex just-content-center align-items-center" v-show="isChooseTemp">
					<image src="../../static/img/index/frame.png" mode="" ></image>
					<view class="choose-temp-item" style="margin-right: 20px;" :class="{active:!chooseTempIndex}" @click="chooseTempClick(0)">圆圈模板</view>
					<view class="choose-temp-item" style="margin-left: 20px;" :class="{active:chooseTempIndex}" @click="chooseTempClick(1)">方块模板</view>
				</view>
			</view>
			<view class="date">
				<view>2020年10月30日</view>
				<view class="d-flex justify-content-between">
					<text>星期四</text>
					<text>10:10</text>
				</view>
			</view>
		</view>
		<uni-swiper-dot :info="info" :current="current" :dots-styles="dotsStyles" mode="dot" field="content" class="" >
			<swiper class="swiper-box" @change="change">
				<swiper-item v-for="(item, index) in info" :key="index" >
					<view :class="item.colorClass" class="swiper-item w-100 h-100">
						<view class="d-flex justify-content-between flex-wrap" >
							<view class="button-item d-flex align-items-center just-content-center" v-for="(child, childIndex) in item" :key="childIndex" @click="navTo(childIndex)">
								<image :src="chooseTempIndex?'../../static/img/index/button-square.png':'../../static/img/index/button-circular.png'" mode=""></image>
								<text class="button-item-text">{{child}}</text>
							</view>
						</view>
					</view>
				</swiper-item>
			</swiper>
		</uni-swiper-dot>
	</view>
</template>

<script>
	export default {
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
				info:[['公司介绍','智能导诊','科室介绍','楼层指引','就诊指引']],
				isChooseTemp:false,
				chooseTempIndex:0,
				urlList:['../compony/compony','../guidance/guidance','../department/department','../floor/floor','../visit/visit']
			}
		},
		onLoad() {

		},
		methods: {
			change(e) {
			    this.current = e.detail.current;
			},
			//显示模板
			showChooseTemp(){
				this.isChooseTemp = !this.isChooseTemp;
			},
			//选择模板
			chooseTempClick(data){
				if(this.chooseTempIndex != data){
					this.chooseTempIndex = data;
					this.isChooseTemp = false;
				}
			},
			//跳转
			navTo(index){
				if(index==0){
					uni.setStorageSync('temData',{
						menu:[
							{name:'公司介绍',url:'../compony/compony'},
						],
						src:'../../static/img/company-profile.png'
					})
				}
				uni.navigateTo({
					url: this.urlList[index],
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style lang="scss">
	.container{
		background-image: url(../../static/img/index/bg.png) ;
	}
	.top{
		height: 8%;
		margin: 0 30px;
		.logo{
			height: 71px;
			width: 294px;
		}
		.top-icon{
			width: 91px;
			height: 76px;
		}
		.choose-temp{
			position: absolute;
			top: 100px;
			width: 500px;
			height: 218px;
			
			image{
				position: absolute;
				height: 100%;
				width: 100%;
				z-index: 1;
			}
			
			.choose-temp-item{
				background: rgb(193,175,160);
				color: #fff;
				z-index: 10;
				font-size: 33px;
				height: 120px;
				padding: 0 20px;
				line-height: 120px;
				border-radius: 10px;
				box-shadow: 5px 5px 5px rgba(0, 0, 0, 0.35)
			}
			.active{
				background: rgba(204, 153, 51, 1);
			}
			
		}
		.date{
			font-size: 70rpx;
		}
	}
	.swiper-box{
		height: 1700px;
		margin-top: 20px;
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
			}
			image{
				width: 350px;
				height: 350px;
			}
		}
		
	}
</style>
