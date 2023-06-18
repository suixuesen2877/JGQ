<template>
	<view class="user-content">
		
		<image src="@/static/img/icon-juan.png" class="header"></image>
		<u-cell-group>
			<u-cell
			    size="large"
			    title="设置"
			    isLink
				url="/pages/setting/setting"
			></u-cell>
		</u-cell-group>
	</view>
</template>

<script>
	export default {
		data() {
			return {
			};
		}
	}
</script>

<style scoped lang="scss">
.user-content {
	.header {
		width: 200rpx;
		height: 200rpx;
		border-radius: 50%;
		margin: 80rpx auto;
		display: block;
	}
}
</style>
