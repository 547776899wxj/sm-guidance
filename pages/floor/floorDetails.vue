<template>
	<view class="container">
		<headerFrom :menu='menu' @redirectToFrom='redirectToFrom'></headerFrom>
		<view class="content">
			<view class="content">
				<view class="content-item d-flex" v-for="(item,index) in floorData" :key="index">
					<view class="item-number d-flex align-items-center just-content-center" :style="(index+1)%2===0?'background-color:#c1afa0':''">
						{{item.number}}
					</view>
					<view class="name-list d-flex flex-wrap " >
						<view class="name" v-for="(child,childIndex) in item.data" :key="childIndex" @click="navTo(child)">
							{{child.name}}
						</view>
					</view>
				</view>
				
			</view>
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
					{name:'楼层指引',url:'../floor/floor'}
				],
				floorData:[
					{
						number:'1F',
						data:[
							{name:'收费处'},
							{name:'中药房'},
							{name:'西药房'},
							{name:'服务台'},
							{name:'儿科'},
							{name:'急诊科'},
							{name:'名医工作室'},
							{name:'住院服务中心'},
						]
					},
					{
						number:'2F',
						data:[
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
						]
					},
					{
						number:'3F',
						data:[
							{name:'普外科'},
							{name:'肛肠科'},
							{name:'骨伤科'},
							{name:'泌尿科'},
							{name:'空腔科'},
							{name:'男科'},
							{name:'皮肤科'},
							{name:'神经外科'},
							{name:'妇科'},
							{name:'妇产科'},
							{name:'医学美容科'},
						]
					},
					{
						number:'4F',
						data:[
							{name:'耳鼻喉科'},
							{name:'眼科'},
							{name:'疼痛科'},
							{name:'麻醉科'},
							{name:'肿瘤科'},
							{name:'手术科'},
							{name:'医学影像科'},
							{name:'彩超室'},
						]
					},
					{
						number:'5F',
						data:[
							{name:'行政中心'},
						]
					}
				]
			};
		},
		onLoad(e) {
			let name = uni.getStorageSync('floorName');
			if(name){
				this.menu[1] = {name:name,url:'../floor/floorDetails'}
			}
			
		},
		methods:{
			//导航栏跳转
			redirectToFrom(url){
				uni.redirectTo({
					url: url,
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			},
			//跳转
			navTo(data){
				uni.setStorageSync('temData',{
					menu:this.menu,
					src:'../../static/img/test/floor.jpg'
				})
				uni.navigateTo({
					url: '../compony/compony',
					success: res => {},
					fail: () => {},
					complete: () => {}
				});
			}
		}
	}
</script>

<style lang="scss">
	.content{
		.content-item{
			padding: 20px 20px 0 20px;
			color: #fff;
			.item-number{
				background-color: $base-ccolor;
				font-size: 60px;
				width: 20%;
				text-align: center;
				border-radius: 10px;
			}
			.name-list{
				width: 80%;
				border: 1px solid $base-ccolor;
				border-radius: 10px;
				padding: 10px 0;
				.name{
					background-color: $base-ccolor;
					font-size: 32px;
					text-align: center;
					padding: 10px 0;
					width: 186px;
					height: 62px;
					overflow: hidden;
					box-sizing: border-box;
					border-radius: 100px;
					margin: 20px 10px;
				}
			}
		}
		
	}
</style>

