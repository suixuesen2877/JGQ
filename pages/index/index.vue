<template>
	<view class="content">
		<view class="header">总次数：{{total}}</view>
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
			
		};
	},
	onLoad() {},
	methods: {
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
	.header {
		line-height: 40rpx;
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
