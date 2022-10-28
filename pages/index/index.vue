<template>
	<view class="content">
		<view style="height: 100rpx;" class=""></view>
		<view class="tools">
			<image @click="show = true" class="icon-setting" src="@/static/setting.png" mode=""></image>
		</view>
		<view style="height: 300rpx;" class=""></view>
		<view class="list">
			<view v-for="(item,index) of list" :key="index" class="list-item">
				{{item}}
			</view>
		</view>
		<image @click="woodFishHandle" :class="status === 1?'wooden_fish_act':''" class="wooden_fish" src="@/static/muyu.png" mode=""></image>
		<view class="auto">
			<button @click="auto" v-if="status === 0">自动功德</button>
			<button @click="close" v-if="status === 1">关闭自动功德</button>
		</view>
		<u-popup mode="left" :show="show" @close="setting_close" @open="setting_open">
			<view class="setting-block">
				<input class="inp" type="text" placeholder="例:功德 +1" v-model="text" name="" id="">
			</view>
		</u-popup>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				title: 'Hello',
				audio: require("@/static/audio.mp3"),
				list: [],
				timer: null, //定时器
				status: 0, //状态
				show: false,
				text:"功德 +1",
			}
		},
		onLoad() {

		},
		methods: {
			woodFishHandle() {
				let _this = this
				this.list.push(_this.text)
				const innerAudioContext = uni.createInnerAudioContext();
				innerAudioContext.autoplay = true;
				innerAudioContext.src = this.audio;
				innerAudioContext.onPlay(() => {
					console.log('开始播放');
				});
			},
			auto() {
				let _this = this
				_this.status = 1
				_this.timer = setInterval(function() {
					_this.woodFishHandle()
				}, 200)
			},
			close() {
				let _this = this
				_this.status = 0
				clearInterval(_this.timer)
			},

			setting_open() {
				// console.log('open');
			},
			setting_close() {
				this.show = false
				// console.log('close');
			}
		}
	}
</script>

<style>
	@keyframes text-animation {

		from {
			top: 0;
		}

		to {
			top: -300rpx;
			opacity: .0;
		}

	}
	@keyframes fish-animation {
	
		from {
			transform: scale(1);
		}
	
		to {
			transform: scale(1.2);
		}
	
	}

	page {
		background-color: #202020;
	}

	.content {
		position: relative;
		height: 100vh;
	}

	.wooden_fish {
		width: 260rpx;
		height: 199rpx;
		position: absolute;
		left: 50%;
		top: 50%;
		margin-left: -130rpx;
		margin-top: -99.5rpx;
	}
	.wooden_fish_act{
		animation: fish-animation linear  .1s infinite alternate;
	}
	.wooden_fish:active {
		transform: scale(1.2);
	}

	.list {
		text-align: center;
		color: #fff;
		position: relative;
		display: flex;
		justify-content: center;

	}

	.list-item {
		position: absolute;
		animation: text-animation linear .5s forwards;
	}

	.auto {
		position: fixed;
		bottom: 100rpx;
		width: 100%;
		display: flex;

	}

	.tools {
		height: 100rpx;
		padding-left: 50rpx;
		box-sizing: border-box;
	}

	.icon-setting {
		width: 50rpx;
		height: 50rpx;
	}
	.setting-block{
		width: 500rpx;
		padding: 20rpx;
		box-sizing: border-box;
	}
	.inp{
		border: 1px solid #eee;
		border-radius: 20rpx;
		height: 72rpx;
		padding: 6rpx 20rpx;
		font-size: 28rpx;
	}
</style>
