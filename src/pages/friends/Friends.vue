<template>
	<view>
		<view>
			通讯录
		</view>
		<view ><button type="primary" @longtap="vibrateShort()">震动</button></view>
		<view ><button type="primary" @click="go()">打电话</button></view>
	</view>
</template>

<script>
	export default {
		data () {
			return {
				result: ''
			}
		},
		onLoad() {
		},
		methods: {
			go(){
			 	uni.makePhoneCall({
			 	
			 	// 手机号
			    phoneNumber: '18320295575', 
			
				// 成功回调
				success: (res) => {
					console.log('调用成功!')	
				},
			
				// 失败回调
				fail: (res) => {
					console.log('调用失败!')
				}
				
			  });
			},
			vibrateShort() {
							uni.vibrateShort({
								success: function() {
									console.log('success');
								}
							});
			}
			// checkIsSupportSoterAuthentication(){
			// 		// #ifdef APP-PLUS || MP-WEIXIN
			// 		uni.checkIsSupportSoterAuthentication({
			// 			success(res) {
			// 			    console.log(res);
			// 				// 如果当前设备支持生物识别方式，且支持指纹识别方式
			// 				if(res.supportMode && res.supportMode.includes('fingerPrint')){
			// 					/** 
			// 					 * uni.checkIsSoterEnrolledInDevice : 获取设备内是否录入指纹信息
			// 					 *  checkAuthMode: 'fingerPrint', // 检验指纹信息
			// 					 * */
			// 					uni.checkIsSoterEnrolledInDevice({
			// 					    checkAuthMode: 'fingerPrint', // 检验指纹信息
			// 					    success(res) {
			// 					        console.log(res.isEnrolled)
			// 							if(res.isEnrolled == true){
			// 								/** 
			// 								 * 开始 SOTER 生物认证
			// 								 * 执行成功，进行后续操作
			// 								 * */
			// 								uni.startSoterAuthentication({
			// 									requestAuthModes: ['fingerPrint'],
			// 									challenge: '123456',
			// 									authContent: '请用指纹解锁',
			// 									success(res) {
			// 										console.log(res);
			// 										uni.showToast({
			// 											title: "识别成功",
			// 											duration: 3000,
			// 											icon:'none'
			// 										})
			// 										//指纹识别成功后，进行后续工作
			// 									},
			// 									fail(err) {
			// 										uni.showToast({
			// 											title: "识别失败",
			// 											duration: 3000,
			// 											icon:'none'
			// 										})
			// 									},
			// 									complete(res) {
			// 										console.log(res);
			// 									}
			// 								})
			// 							}else{
			// 								this.result = '此设备未录入指纹，请到设置中开启';
			// 							}
			// 					    },
			// 						fail(err) {
			// 					        uni.showModal({
			// 					        	title:'温馨提示',
			// 					        	content:'此设备未录入指纹，请到设置中开启',
			// 								showCancel: false,
			// 					        	success:function(res){
			// 									// 进行后续逻辑
			// 					        	}
			// 					        })
			// 					    }
			// 					})
								
			// 				}
			// 				else{
			// 					this.result = "此设备不支持指纹识别功能"
			// 				}
			// 			},
			// 			fail(err) {
			// 				uni.showModal({
			// 					title:'温馨提示',
			// 					content:'此设备不支持指纹识别功能',
			// 					showCancel: false,
			// 					success:function(res){
			// 						// 进行后续逻辑
			// 					}
			// 				})
			// 			}
			// 		})
			// 		// #endif
					
			// 		// #ifndef APP-PLUS || MP-WEIXIN
			// 		this.result = '此平台不支持指纹识别';
			// 		// #endif
			// 	}
		}
	}
</script>

<style>
</style>
