<template>
	<view class="container">
		<view class="container uni-center">
			<view class="intro">请输入数字(1-10)</view>
			<view class="uni-flex uni-row" style="justify-content: center;">
				<view class="flex-item uni-bg-green"><input type="number" v-model="num1" maxlength="2" style="width: 50px;"></view>
				<view class="flex-item"><input type="number" maxlength="1" style="width: 10px;" disabled="true"></view>
				<view class="flex-item uni-bg-red"><input type="number" v-model="num2" maxlength="2" style="width: 50px;"></view>
				<view class="flex-item"><input type="number" maxlength="1" style="width: 10px;" disabled="true"></view>
				<view class="flex-item uni-bg-green"><input type="number" v-model="num3" maxlength="2" style="width: 50px;"></view>
				<view class="flex-item"><input type="number" maxlength="1" style="width: 10px;" disabled="true"></view>
				<view class="flex-item uni-bg-red"><input type="number" v-model="num4" maxlength="2" style="width: 50px;"></view>
			</view>
			<br/>
			<view class="uni-flex uni-row">
				<button type="primary" @click="calc">计算</button> 
				<button type="default" @click="clear">清空</button>
			</view>
		</view>
		<view class="intro">计算结果</view>
		<text style="color: #66AAFF;">{{text}}</text>
	</view>
</template>

<script>
	// import { calc24 } from '@/common/calc24.js';
	var calc24 = require('@/common/calc24.js');  //require这个js模块
	
	export default {
		data() {
			return {
			num1: '',
			num2: '',
			num3: '',
			num4: '',
			text: ''
				}
		},
		methods: {
			validNum(num){
				return num>0 && num<=10;
			},
			calc(){
				if (this.num1.length==0 ||
				this.num2.length==0 ||
				this.num3.length==0 ||
				this.num4.length==0 
				){
					uni.showModal({
					    title: '提示',
					    content: '必须输入4个1~10的数字'
					});
				}else{
					if(!this.validNum(this.num1) ||
					!this.validNum(this.num2) ||
					!this.validNum(this.num3)||
					!this.validNum(this.num4)){
						uni.showModal({
						    title: '提示',
						    content: '必须输入4个1~10的数字'
						});
						return;
					}
					var res = calc24.get24(this.num1,this.num2,this.num3,this.num4);
					if(res.length == 0){
						this.text = "无法得出"
					}else{
						var info = "共"+res.length+"结果\n";
						for(var n=0;n<res.length; n++){
							info += res[n] + "\n";
						}
						this.text = info;
					}
				};
				
			},
			clear(){
				this.num1 = '';
				this.num2 = '';
				this.num3 = '';
				this.num4 = '';
			},
		}
	}
</script>

<style>
	.container {
		padding: 20px;
		font-size: 14px;
		line-height: 24px;
	}
</style>
