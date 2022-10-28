<template>
	<view class="content">
	<view style="height: 500rpx;" class=""></view>
	<view class="list">
		<view v-for="(item,index) of list" :key="index" class="list-item">
			{{item}}
		</view>
	</view>
	 <image @click="woodFishHandle" class="wooden_fish" src="@/static/muyu.png" mode=""></image>
	</view>
</template>

<script>
	
	export default {
		data() {
			return {
				title: 'Hello',
				audio:require("@/static/audio.mp3"),
				list:[]
			}
		},
		onLoad() {
			
		},
		methods: {
			woodFishHandle(){
				let _this = this
				this.list.push("功德 +1")
				const innerAudioContext = uni.createInnerAudioContext();
				innerAudioContext.autoplay = true;
				innerAudioContext.src =  this.audio;
				innerAudioContext.onPlay(() => {
				  console.log('开始播放');
				});
			}
		}
	}
</script>

<style>
	 @keyframes fish-animation {
	 
	    from {
	         top: 0;
	     }
	     to {
	         top: -300rpx;
			 opacity: .0;
	     }
	 
	 }
	 page{
		 background-color: #202020;
	 }
	 .content{
		 position: relative;
		 height: 100vh;
	 }
	 .wooden_fish{
		 width: 260rpx;
		 height: 199rpx;
		 position: absolute;
		 left: 50%;
		 top: 50%;
		 margin-left: -130rpx;
		 margin-top: -99.5rpx;
	 }
	 .wooden_fish:active{
		 transform: scale(1.2);
	 }
	 .list{
		 text-align: center;
		 color: #fff;
		 position: relative;
		 display: flex;
		 justify-content: center;
		
	 }
	 .list-item{
		 position: absolute;
		 animation: fish-animation linear .5s forwards;
	 }
</style>
