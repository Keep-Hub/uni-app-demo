<template>
	<view>
		<view>我的</view>
		<view><button type="primary" @click="toCeshi()">{{title}}</button></view>
		<view><button type="primary" @click="getDeviceInfo()">获取手机信息</button></view>
		<view>
			<view><text>手机型号: {{deviceInfo.model}}</text></view>
			<view><text>设备像素比: {{deviceInfo.pixelRatio}}</text></view>
			<view><text>语言: {{deviceInfo.language}}</text></view>
			<view><text>操作系统版本: {{deviceInfo.system}}</text></view>
			<view><text>客户端平台: {{deviceInfo.platform}}</text></view>
		</view>
		<view><button type="primary" @click="getNetworkType()">获取手机网络信息</button></view>
		<view>
			<view><text>手机网络类型: {{networkType.networkType}}</text></view>
		</view>
	</view>
</template>

<script>
	export default {
		data () {
			return {
				title: "测试跳转",
				deviceInfo: '',
				networkType: ''
			}
		},
		onLoad() {
		
		},
		methods: {
			toCeshi () {
				uni.navigateTo({
					url: '../test/test',
					success: res => {},
					fail: () => {},
					complete: () => {}
				})
			},
			getDeviceInfo () {
				this.deviceInfo = this._getDeviceInfo()
			},
			getNetworkType() {
				this.networkType = this._getNetworkType()
			},
			_getNetworkType() {
				let result = 0
				uni.getNetworkType({
				        success (res) {
							result = res;
				            console.log(res.networkType);
				        }
				    });
					return result;
			},
			_getDeviceInfo () {
				// 获取设备信息
				let result = 0
				uni.getSystemInfo({
				        success (res) {
							result = res;
				            // console.log(res.model);              //手机型号
				            // console.log(res.pixelRatio);   		//设备像素比
				            // console.log(res.windowWidth);  	//可使用窗口宽度
				            // console.log(res.windowHeight);  //可使用窗口高度
				            // console.log(res.language);   		//应用设置的语言
				            // console.log(res.system);    			//操作系统版本
				            // console.log(res.platform);   		//客户端平台，值域为：ios、android
				        }						
				    });
					return result;
			}
		}
	}
</script>

<style>
</style>
