<template>
	<view class="container">
		<headerFrom :menu='menu' @redirectToFrom='redirectToFrom'></headerFrom>
		<view class="content">
			<view class="content-frame box-shadow-basics">
				<view class="frame-title">
					{{menu[1].name}}
				</view>
				<view class="frame-details">
					 脾胃病科长期以来坚持以中医为主导中西医结合的方向，开展消化系统疾病的诊断治疗、临床教学和科研工作。科室共有医学专业人员14人，其中主任医师4人，副主任医师2人，主治医师4人，住院医师4人。科内设有脾胃病科病房、脾胃病科门诊、消化功能检测室，并协同消化内镜科完成电子胃镜、电子结肠镜等内镜下检查及治疗工作。临床诊疗中注重中医辨证论治，结合现代医学先进的诊断治疗方法，对疾病进行中西医诊断及治疗，中西医结合治疗食管、胃、肠、肝、胆、胰腺等疾病有良好的疗效，尤其对慢性萎缩性胃炎、消化性溃疡、功能性胃肠疾病、炎症性肠病、急慢性胰腺炎、急慢性肝炎等有独到的疗效，用中西医结合的综合治疗方法治疗疑难杂症和抢救危重病患者，深得患者及家属的好评。在多年实践中自主研制的藿砂口服液、胃炎胶囊、五倍子液、白芨胶浆和吉祥膏方（健脾和胃膏）疗效好、副作用低，临床应用方便。消化功能检测室常规开展胃幽门螺杆菌检测、胃肠电生理检测、胶囊内镜检查，并协同消化内镜科完成电子胃镜、电子结肠镜等内镜下检查及治疗工作。脾胃病科全体医护人员始终以良好的素质、精湛的技术、先进的仪器设施为消化系统疾病患者提供优质的医疗服务。
				</view>
			</view>
			<view class="doctor">
				<view class="doctor-list d-flex flex-wrap">
					<view class="doctor-item d-flex align-items-center justify-content-between flex-column" v-for="(item,index) in doctorData " :key="index" :style="((index+1)%3)!=0?'margin-right: 45px;':''" @click="showDoctor(item.id)">
						<image src="../../static/img/doctor.png" mode=""></image>
						<view class="doctor-text">{{item.name}}</view>
					</view>
				</view>
			</view>
		</view>
		<view class="doctor-modul" v-show="isModul" @click="isModul=false">
			<view class="doctor-modul-content">
				<image class="modul-bg" src="../../static/img/bg-noframe.png" mode=""></image>
				<view class="doctor-modul-details">
					<view class="modul-content-header d-flex ">
						<image class="doctor-img" src="../../static/img/test/doctor.png" mode=""></image>
						<view class="content-header-info d-flex flex-column just-content-center">
							<view class="info-text d-flex">
								<view class="info-text-title"><text>姓</text><text>名：</text></view>
								<view>阙庆辉</view>
							</view>
							<view class="info-text d-flex mt-80">
								<view class="info-text-title"><text>职</text><text>称：</text></view>
								<view>主任医师</view>
							</view>
							<view class="info-text d-flex mt-80">
								<view class="info-text-title">所属科室：</view>
								<view>针灸部</view>
							</view>
						</view>
					</view>
					<view class="modul-content-bottom">
						<view class="content-bottom-item d-flex">
							<view class="bottom-item-title d-flex justify-content-between"><text>擅</text><text>长：</text></view>
							<view class="bottom-item-content">颈椎病、腰椎间盘突出症、骨性关节炎、中风后遗症、面瘫、偏头痛等疾病的康复治疗。</view>
						</view>
						<view class="content-bottom-item d-flex">
							<view class="bottom-item-title d-flex justify-content-between"><text>门诊时间：</text></view>
							<view class="bottom-item-content">星期二上午,星期二下午,星期四上午,星期五上午,星期五下午,星期六上午</view>
						</view>
						<view class="content-bottom-item d-flex">
							<view class="bottom-item-title d-flex justify-content-between"><text>诊</text><text>室：</text></view>
							<view class="bottom-item-content">康复楼（五号楼）四楼针灸部诊室1</view>
						</view>
						<view class="content-bottom-item d-flex">
							<view class="bottom-item-title d-flex justify-content-between"><text>个人简介：</text></view>
							<view class="bottom-item-content">中国针灸学会临床分会理事、中国针灸学会临床分会痛症委员会副主任委员、福建省针灸学会常务理事。从医20多年，具有丰富的临床诊疗经验，知名针灸康复专家。</view>
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
					{name:'科室介绍',url:'../department/department'},
					{name:'脾胃病科'},
				],
				doctorData:[
					{name:'张医生',id:1},
					{name:'吴医生',id:2},
					{name:'陈医生',id:3},
				],
				isModul:false,
			};
		},
		onLoad(e) {
			if(e.name){
				this.menu[1].name = e.name;
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
			showDoctor(id){
				this.isModul = true;
			}
		}
	}
</script>

<style lang="scss">
	.mt-80{
		margin-top: 80px;
	}
	.doctor-modul{
		background: rgba(0,0,0,0.2);
		width: 100%;
		box-sizing: border-box;
		padding-top: 50px;
		height: calc(100% - 97px);
		position: absolute;
		top: 97px;
		.doctor-modul-content{
			width: 90%;
			margin: auto;
			box-sizing: border-box;
			position: 40px 10px;
			border-radius: 20px;
			height: 94%;
			overflow: scroll;
			position: relative;
			.modul-bg{
				position: absolute;
				height: 100%;
				width: 100%;
				z-index: 0;
			}
			.doctor-modul-details{
				padding:70px 40px 0 40px;
				position: relative;
				z-index: 100;
				.modul-content-header{
					
					.doctor-img{
						width: 310px;
						padding-right: 88px;
						height: 400px;
					}
					.info-text{
						font-size: 50px;
						color: #000000;
						z-index: 100;
					}
					.info-text-title{
						width: 250px;
						display: flex;
						justify-content: space-between;
					}
				}
				.modul-content-bottom{
					font-size: 42px;
					padding-top: 20px;
					.content-bottom-item{
						padding-top: 60px;
						.bottom-item-title{
							width: 210px;
							flex: 1;
						}
						.bottom-item-content{
							width: 680px;
						}
					}
				}
			}
			
		}
	}
	.doctor{
		width: 90%;
		margin:110px auto;
		.doctor-list{
			.doctor-item{
				background: #c1afa0;
				height: 420px;
				width: 290px;
				border-radius: 10px;
				image{
					padding-top: 30px;
					width: 94%;
					height: 60%;
					
				}
				.doctor-text{
					color: #fff;
					font-size: 50px;
					padding-bottom: 20px;
				}
			}
		}
	}
	.container{
		background-image: url(../../static/img/bg-noframe.png) ;
	}
	.content{
		margin-top: 50px;
		.content-frame{
			width: 90%;
			margin: auto;
			border: 1px solid #797979;
			background-color: #fff;
			font-size: 53px;
			border-radius: 20px;
			.frame-title{
				font-weight: bold;
				text-align: center;
				padding: 30px 0;
			}
			.frame-details{
				padding: 0px 10px 20px 30px;
				height: 500px;
				font-size: 50px;
				overflow: scroll;
			}
		}
	}
</style>
