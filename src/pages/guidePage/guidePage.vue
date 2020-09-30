<template>
	<view class="guide-page">
		<swiper :indicator-dots="true" :autoplay="false" :interval="3000" :duration="800" style="height: 100%;">
			<swiper-item>
				<view class="swiper-item">
					<image :style="{'height':windowHeight}" style="width: 100%;" src="../../static/loading.png" mode=""></image>
				</view>
			</swiper-item>
			<swiper-item>
				<view class="swiper-item">
					<button plain="true" style="width: 100%;position: fixed;bottom: 50rpx;z-index: 99; padding: 0 10rpx;" type="primary" @click="toStart()">开始</button>
					<image :style="{'height':windowHeight}" style="width: 100%;" src="../../static/loading.png" mode=""></image>
				</view>
			</swiper-item>
		</swiper>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				windowHeight: "200px"
			}
		},
		onLoad() {
			uni.getSystemInfo({
			
			    success: (res) => {
			
			        this.windowHeight = res.windowHeight+"px";
			
			} })
		},
		methods: {
			toStart() {
				uni.switchTab({
					url: '../index/index',
					success: res => {},
					fail: () => {},
					complete: () => {}
				})
			}
		}	
	}
</script>

<style>
	page,.guide-page{
		width: 100%;
		height: 100%;
	}
</style>
