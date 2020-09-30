<template>
</template>

<script>
	export default {
		components: {
		        },
		data() {
			return {}
		},
		onLoad() {
			const value = uni.getStorageSync('launchFlag');
			if (value) {
				uni.switchTab({
					url: '../index/index'
				})
			} else {
				uni.setStorage({
					key: "launchFlag",
					data: true
				});
				uni.redirectTo({
					url: '../guidePage/guidePage'
				})
			}
		},
		methods: {}
	}
</script>

<style>
</style>
