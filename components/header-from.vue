<template>
	<view>
		<view class="header d-flex">
			<view class="index header-item d-flex just-content-center" @click="navTo('../index/index')">
				<image src="../static/img/home.png" mode=""></image>
				<text >首页</text>
			</view>
			<view class="header-item d-flex just-content-center"  v-for="(item,index) in menu" :key="item.name" :style="index == 0 ?'padding-left: 20px;':''"  @click="navTo(item.url)">
				<text class="arrow" v-if="index > 0"> >> </text>
				<image src="../static/img/from.png" mode=""></image>
				<text>{{item.name}}</text>
			</view>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			};
		},
		props:{
			menu:{
				type:Array,
				default () {
					return []
				}
			}
		},
		methods:{
			//跳转
			navTo(url){
				this.$emit('redirectToFrom',url);
			}
		}
	}
</script>

<style lang="scss">
	.header{
		.header-item.index{
			background-color: #ac937e;
			color: #fff;
			padding: 20px 30px;
		}	
		.header-item{
			padding: 20px 30px 20px 0;
			font-size: 34px;
			text-align: center;
			border-bottom: 7px solid #ac937e;
			color: #C1AFA0;
		}
		.arrow{
			padding-right: 20px;
		}
		image{
			width: 52px;
			height: 50px;
			margin-right: 20px;
		}
		text{
			padding-top: 4px;
		}
	}
</style>
