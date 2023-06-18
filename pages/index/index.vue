<template>
	<view class="content">
		<view class="hint">
			<view class="item">
				赚几个逼子儿：
				<view><image src="../../static/img/icon-money.svg"></image><text>{{fuckMoney}}</text></view>
			</view>
			<view class="item">
				距离下班：
				<view class=""><image src="../../static/img/icon-time.svg"></image><text>{{happyTime}}</text></view>
			</view>
			
		</view>
		<view class="total">摸鱼次数：{{total}}</view>
		<image class="fish" src="/static/img/yu1.png" mode="widthFix" @click="handleClick"></image>
		<view class="tap-num" v-if="tapNum > 0">{{tapNum}}</view>
	</view>
</template>

<script>
export default {
	data() {
		return {
			tapNum: 0,
			total: 0,
			timer: null,
			multiple: 1,
			fuckMoney: '**',
			happyTime: '****'
		};
	},
	onLoad() {},
	onShow() {
		let setting = getApp().globalData.setting
		
		const date = this.$moment().format('YYYY-MM-DD')
		// setting = {
		// 	emoTime: '16:00',
		// 	happyTime: '23:00',
		// 	fuckMoney: 1000
		// }
		const salary = setting.fuckMoney // 日薪
		let emoTime = this.$moment(new Date(`${date} ${setting.emoTime}`)).format('X')
		let happyTime = this.$moment(new Date(`${date} ${setting.happyTime}`)).format('X')
		let now = this.$moment().format('X')
		
		if( now < emoTime) {
			console.log('还可以耍')
		} else if(now > happyTime) {
			console.log('接着耍')
		} else {
			console.log('上坟中')
			let workTime = now - emoTime // 已工作时长
			let duration = happyTime - emoTime // 日工作时长
			let surplus = happyTime - now // 剩余时长
			let ms = (salary/duration).toFixed(2) - 0 // 秒薪
			this.fuckMoney = (ms * workTime).toFixed(2) - 0
			console.log()
			
			setInterval(() => {
				surplus -= 1
				let x = this.$moment.duration(surplus*1000)._data
				this.fuckMoney = (this.fuckMoney + ms).toFixed(2) - 0
				this.happyTime = `${x.hours} : ${x.minutes} : ${x.seconds}`
			}, 1000)
		}
	},
	
	mounted() {
		
	},
	methods: {
		handleSetting() {
			
		},
		handleClick() {
			const r = Math.floor(Math.random()*100)
			if(r > 90 && this.tapNum > 5) this.multiple = this.multiple * 2
			this.tapNum += (1 * this.multiple)
			clearTimeout(this.timer);
			this.timer = setTimeout(()=> {
				this.handleAdd()
			}, 2000)
		},
		handleAdd() {
			this.total += this.tapNum
			this.tapNum = 0
		},
	}
};
</script>

<style scoped lang="scss">
.content {
	position: relative;
	.hint {
		padding: 36rpx;
		display: flex;
		justify-content: space-between;
		.item {
			padding: 20rpx 30rpx;
			line-height: 80rpx;
			font-size: 34rpx;
			border-radius: 20rpx;
			box-shadow: 10rpx 10rpx 30rpx 6rpx rgba(0, 0, 0, 0.1);
			view {
				width: 100%;
				margin: auto;
				display: flex;
				justify-content: center;
				align-items: center;
				image {
					width: 50rpx;
					height: 50rpx;
					margin-right: 10rpx;
				}
				text {
					width: 200rpx;
				}
			}
		}
	}
	.total {
		padding: 36rpx 36rpx;
	}
	.fish {
		width: 240rpx;
		margin: 240rpx auto;
		display: block;
		animation: swim 5s linear infinite;
	}
	.tap-num {
		position: absolute;
		right: 20rpx;
		top: 40rpx;
	}
	@keyframes swim {
		0% {
			transform: translate(0, 0) rotate(0deg);
		}
		24% {
			transform: translate(-100px, 50px) rotate(0deg);
		}
		25% {
			transform: translate(-100px, 50px) rotate(180deg);
		}

		50% {
			transform: translate(0, 0) rotate(180deg);
		}

		74% {
			transform: translate(100px, -50px) rotate(180deg);
		}
		75% {
			transform: translate(100px, -50px) rotate(0deg);
		}
		100% {
			transform: translate(0, 0) rotate(0deg);
		}
	}
}
</style>
