<template>
	<view class="setting">
		<u-form labelPosition="left" :model="settingData" :rules="rules" ref="uForm">
			<u-form-item label="日薪: " prop="fuckMoney" borderBottom ref="fuckMoney">
				<u-input v-model="settingData.fuckMoney" border="none" placeholder="请输入"></u-input>
			</u-form-item>
			<u-form-item label="上坟时间: " prop="emoTime" borderBottom ref="emoTime" @click="showEmoPicker = true">
				<u-input v-model="settingData.emoTime" disabled border="none" placeholder="请输入"
					@click="showEmoPicker = true"></u-input>
			
			</u-form-item>
			<u-form-item label="下班时间: " prop="happyTime" borderBottom ref="happyTime" @click="showHappyPicker = true">
				<u-input v-model="settingData.happyTime" disabled border="none" placeholder="请输入"
					@click="showHappyPicker = true"></u-input>

			</u-form-item>
			<u-datetime-picker :show="showEmoPicker || showHappyPicker" v-model="time" mode="time"
				@cancel="showPicker = false" @confirm="handleSetDate"></u-datetime-picker>

		</u-form>
		<u-button text="保存" type="primary" class="save" @click="handleSave"></u-button>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				showEmoPicker: false,
				showHappyPicker: false,
				settingData: {
					emoTime: '',
					happyTime: '',
					fuckMoney: null
				},
				time: '',
				rules: [],
			};
		},
		methods: {
			handleSetDate(v) {
				if(this.showEmoPicker) this.settingData.emoTime = v.value
				if(this.showHappyPicker) this.settingData.happyTime = v.value
				this.showEmoPicker = false
				this.showHappyPicker = false
			},
			handleSave() {
				getApp().globalData.setting = this.settingData
				console.log(this.settingData)
				uni.navigateBack()
			}
		}
	}
</script>

<style scoped lang="scss">
	.setting {
		height: 85vh;
		box-sizing: border-box;
		padding: 40rpx;
		display: flex;
		flex-direction: column;
		justify-content: space-between;

		.save {}
	}
</style>