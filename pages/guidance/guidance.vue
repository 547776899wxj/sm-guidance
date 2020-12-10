<template>
	<view class="container">
		<headerFrom :menu='menu' @redirectToFrom='redirectToFrom'></headerFrom>
		<view class="bg d-flex just-content-center align-items-center" v-show="stepNumber===0">
			<image class="w-100 h-100" src="../../static/img/guidance/guidance1.jpg" mode=""></image>
			<view class="first-button" @click="step()"></view>
		</view>
		<view class="bg" v-show="stepNumber===1">
			<image class="w-100 h-100" src="../../static/img/guidance/guidance2.jpg" mode=""></image>
			<view class="second-button" @click="step()"></view>
		</view>
		<view class="bg" v-show="stepNumber===2">
			<image class="w-100 h-100" src="../../static/img/guidance/guidance3.jpg" mode=""></image>
			<view class="d-flex third-button  justify-content-between">
				<view @click="back()"></view>
				<view @click="step()"></view>
			</view>
		</view>
		<view class="bg d-flex just-content-center align-items-center" v-show="stepNumber===3">
			<image class="w-100 h-100" src="../../static/img/guidance/guidance4.png" mode=""></image>
			<view class="fourth-button" @click="step()"></view>
		</view>
		<view class="bg" v-show="stepNumber===4">
			<view class="w-100 h-100 " v-show="inspect==0">
				<image class="w-100 h-100" src="../../static/img/guidance/humanBody.jpg" mode=""></image>
				<view class="humanBody">
					<view class="header humanBody-item">
						
					</view>
				</view>
				<view class="d-flex third-button  justify-content-between">
					<view @click="navTo"></view>
					<view @click="inspect++"></view>
				</view>
			</view>
			<view class="w-100 h-100 " v-show="inspect==1">
				<image class="w-100 h-100" src="../../static/img/guidance/answer.jpg" mode=""></image>
				<view class="answer" @click="inspect++"></view>
			</view>
			<view class="w-100 h-100 " v-show="inspect==2">
				<image class="w-100 h-100" src="../../static/img/guidance/answer1.png" mode=""></image>
				<view class="d-flex answer1 justify-content-between">
					<view  @click="endQuestion"></view>
					<view  @click="endQuestion"></view>
				</view>
			</view>
			<view class="w-100 h-100 " v-show="inspect==3">
				<image class="w-100 h-100" src="../../static/img/guidance/answer2.jpg" mode=""></image>
			</view>
			<view class="w-100 h-100 " v-show="inspect==4">
				<image class="w-100 h-100" src="../../static/img/guidance/answer3.jpg" mode=""></image>
			</view>
			<view class="doctor-modul"  v-show="isModul">
				<view class="doctor-modul-content">
					<view class="modul-content-header">
						<view class="title">
							<text>头晕</text>
							<image class="icon-return" src="../../static/img/guidance/return.png" mode="" @click="isModul=false"></image>
						</view>
						<view class="header-type d-flex align-items-center">
							<image class="icon-proposal" src="../../static/img/guidance/proposal.png" mode=""></image>
							<view class="proposal-title">建议就诊科室：</view>
							<view class="proposal-text box-shadow-basics">神经内科</view>
						</view>
					</view>
					<view class="modul-content-details">
						<text>症状描述：
						    1、头晕耳鸣：兼见面赤、口苦咽干，为肝阳上亢所致;兼见腰膝酸软，遗精健忘者，为肾精亏虚所致。
					
						　　2、头晕目眩：兼寒热、口苦咽干，为外感少阳证;兼面色不华，心悸失眠，为气血亏虚;多在头项运动时发作，颈僵肩沉，甚则活动转侧受限，为三阳脉阻之项痹。
					
						　　3、头晕头痛：恼怒加重者，为风阳、肝火上扰清窍;外伤所致，或舌有瘀点瘀斑者，为瘀血阻络。
					
						　　4、头晕呕吐：舌苔白腻，或眼球震颤者，为痰浊上蒙。
						----------------------------------------------------
						相关信息：
					
						别名:眩晕
					
						患病部位:头部,头颅
					
						细分症状:脑原性头晕、心源性头晕、血管抑制性头晕、药物中毒性头晕
					
						相关疾病:颈椎病、贫血、高血压病、脑动脉硬化、颅脑外伤综合症
					
						相关检查:听力检查、前庭功能检查、眼底检查、颅脑CT
					
						相关症状:贫血、心律失常、心力衰竭、低血压、药物中毒、哮喘
						</text>
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
					{name:'智能导诊',url:'../guidance/guidance'}
				],
				stepNumber:0,
				inspect:0,
				isModul:false,
			};
		},
		methods:{
			//下一步
			step(){
				this.stepNumber++;
			},
			//上一步
			back(){
				this.stepNumber--;
			},
			//结束答题
			endQuestion(){
				this.inspect++;
				setTimeout(()=>{
					this.inspect++;
				},2000)
				setTimeout(()=>{
					this.inspect = 0;
					this.isModul = true;
				},4000)
			},
			//返回首页
			navTo(){
				uni.redirectTo({
					url:'../index/index'
				})
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
		background-image: url(../../static/img/bg-noframe.png);
	}
	.humanBody{
		.humanBody-item{
			background-color: red;
			width: 50px;
			height: 50px;
		}
	}
	.bg{
		width: 100%;
		position: relative;
		height: calc(100% - 97px);
	}
	.first-button{
		position: absolute;
		width: 600px;
		height: 300px;
		z-index: 100;
	}
	.second-button{
		position: absolute;
		width: 200px;
		height: 200px;
		z-index: 100;
		bottom: 128px;
		right: 41%;
	}
	.third-button{
		position: absolute;
		z-index: 100;
		bottom: 128px;
		right: 19%;
		width: 678px;
		view{
			width: 200px;
			height: 200px;
		}
	}
	.fourth-button{
		position: absolute;
		width: 90%;
		z-index: 100;
		height: 500px;
	}
	.answer{
		position: absolute;
		z-index: 100;
		height: 100px;
		width: 300px;
		bottom: 166px;
		right: 37%;
	}
	.answer1{
		position: absolute;
		z-index: 100;
		bottom: 585px;
		right: 10%;
		view{
			height: 100px;
			width: 300px;
		};
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
			border-radius: 30px;
			height: 94%;
			overflow: scroll;
			position: relative;
			background: #fff;
			border: 2px solid $base-ccolor;
			.modul-content-details{
				font-size: 50px;
				overflow: scroll;
				height: calc(100% - 228px);
				padding: 30px;
			}
			.modul-content-header{
				.title{
					color: #fff;
					background-color: $base-ccolor;
					font-size: 50px;
					position: relative;
					text-align: center;
					padding: 28px 0;
				}
				.icon-return{
					width: 55px;
					height: 46px;
					position: absolute;
					right: 70px;
					padding-top: 10px;
				}
				.header-type{
					padding: 20px 30px;
					font-size: 35px;
					margin-top: 4px;
					border-bottom: 1px solid $base-ccolor;
					.icon-proposal{
						height: 38px;
						width: 38px;
						padding-right: 20px;
					}
					.proposal-title{
						color: $base-ccolor;
					}
					.proposal-text{
						color: #fff;
						background: $base-ccolor;
						padding: 10px;
						border-radius: 6px;
						
					}
					
				}
			}
			
		}
	}
</style>
