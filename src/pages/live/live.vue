<template>
	<view class="content">
		<view>直播页</view>
		<image class="logo" src="/static/feicheng.png"></image>
		<view>
			<text class="title">{{title}}</text>
		</view>
		<button  type="primary" @tap="fingerprint()" :disabled="disabled">按下开始识别指纹</button>
		<view style="width: 100%;text-align: center;">
			{{result}}
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				result:"",
				title: '飞橙科技',
				disabled:true
			}
		},
		onLoad() {
			// #ifdef APP-PLUS
			if (!plus.fingerprint.isSupport()) {
				this.result = '此设备不支持指纹识别';
				this.disabled = true;
			}
			else if (!plus.fingerprint.isKeyguardSecure()) {
				this.result = '此设备未设置密码锁屏，无法使用指纹识别';
				this.disabled = true;
			}
			else if (!plus.fingerprint.isEnrolledFingerprints()) {
				this.result = '此设备未录入指纹，请到设置中开启';
				this.disabled = true;
			}
			else {
				this.result = '此设备支持指纹识别';
				this.disabled = false;
			}
			// #endif
			// #ifdef MP-WEIXIN
			this.disabled = false;
			this.result = '请在微信真机中使用，模拟器不支持';
			// #endif
			// #ifndef APP-PLUS || MP-WEIXIN
			this.result = '此平台不支持指纹识别';
			// #endif
		},
		methods: {
			fingerprint: function() {
				// #ifdef APP-PLUS
				plus.fingerprint.authenticate(function() {
					plus.nativeUI.closeWaiting(); //兼容Android平台关闭等待框
					plus.nativeUI.toast('指纹识别成功');
					uni.navigateTo({
						url: '../test/test',
						success: res => {},
						fail: () => {},
						complete: () => {}
					})
				}, function(e) {
					switch (e.code) {
						case e.AUTHENTICATE_MISMATCH:
							plus.nativeUI.toast('指纹识别失败，请重新输入');
							break;
						case e.AUTHENTICATE_OVERLIMIT:
							plus.nativeUI.closeWaiting(); //兼容Android平台关闭等待框
							plus.nativeUI.toast('指纹识别失败次数超出限制，请使用其它方式进行认证');
							break;
						case e.CANCEL:
							plus.nativeUI.toast('已取消识别');
							break;
						default:
							plus.nativeUI.closeWaiting(); //兼容Android平台关闭等待框
							plus.nativeUI.toast('指纹识别失败，请重试');
							break;
					}
				});
				// Android平台手动弹出等待提示框 
				if ('Android' == plus.os.name) {
					plus.nativeUI.showWaiting('指纹识别中...').onclose = function(){
						plus.fingerprint.cancel();
					}
				}
				// #endif
				
				// #ifdef MP-WEIXIN
				wx.startSoterAuthentication({
					requestAuthModes: ['fingerPrint'],
					challenge: '123456',
					authContent: '请用指纹解锁',
					success(res) {
						uni.showToast({
							title: '识别成功',
							mask: false,
							duration: 1500
						});
					}
				})
				// #endif
			},
			
			
			
		}
	}
</script>

<style>
.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin: 200rpx auto 50rpx auto;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>