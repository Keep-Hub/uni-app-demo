<template>
	<view class="chat-home">
		<scroll-view class="main" id="scrollview" scroll-y="false" :style="{height: (style.contentViewHeight*2 + 190) + 'rpx'}" :scroll-with-animation="scrollAnimation" :scroll-top="scrollTop">
					<view v-for="(e,index) in chat" :key="index" class="m-item">
						<view class="left msg" v-if="e.id ==1">
							<image :src="e.img"></image>
							<view class="nr">
								<video v-if="e.video !== ''" class="neir ve"  id="myVideo" :src="e.video"
								     :controls="true"></video>
								<rich-text v-else class="neir" :nodes="e.neir"></rich-text>
								<view class="nt">{{e.name}} {{e.sendTime}}</view>
							</view>
						</view>
						<view class="right msg" v-if="e.id==2">
							<image :src="e.img"></image>
							<view class="nr">
								<video v-if="e.video !== ''" class="neir ve"  id="myVideo" :src="e.video"
								     :controls="true"></video>
								<rich-text v-else class="neir" :nodes="e.neir"></rich-text>
								<view class="nt">{{e.sendTime}}</view>
							</view>					
						</view>
						<view class="center" v-if="e.id==3">
							<view class="inner">{{e.name}}</view>				
						</view>
					</view>	
					<view id='gundong' style='height:1px;width:100%'></view>
				</scroll-view>
				<view class="send">
							<uni-icons class="mic-icon" type="mic" size="24"></uni-icons>
							<!-- <textarea type="text" confirm-type="send" class="chat-send"  v-model="chatm" auto-height="true" show-confirm-bar="false" maxlength="-1" />
							<image src="../../static/send.png" mode="aspectFit" @tap="sendMsg"></image> -->
							<textarea @input="sendChange()" type="text" confirm-type="send" class="chat-send"  v-model="chatm" auto-height="true" show-confirm-bar="false" maxlength="-1" />
							<!-- <image class="smile-icon" src="../../static/smile.png" mode="aspectFit"></image> -->
							<uni-icons class="smile-icon" type="navigate" size="24" @click="sendVideo()"></uni-icons>
							<button v-if="showSendBtn" class="send-icon" type="default" size="mini" @tap="sendMsg()">发送</button>
							<uni-icons v-else class="plus-icon" type="plus" size="24"></uni-icons>
							
				</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				chatm: '',
				showSendBtn: false,
				uid: '',
				fid: '',
				nowTime: new Date().toISOString().slice(0, 10),
				scrollAnimation: false,
				scrollTop: '',
				style: {
				            pageHeight: 0,
				            contentViewHeight: 0,
				            footViewHeight: 90,
				            mitemHeight: 0
				        },
				chat: [
					{
						id: 1,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					},
					{
						id: 2,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话我刚刚说了话我刚刚说了话我刚刚说了话我刚刚说了话我刚刚说了话',
						sendTime: '14:30'
					},
					{
						id: 2,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					},
					{
						id: 1,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					},
					
					{
						id: 2,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					},
					{
						id: 1,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					},
					{
						id: 2,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					},
					{
						id: 1,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					},
					{
						id: 2,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: '我刚刚说了话',
						sendTime: '14:30'
					}
				]
			}
		},
		created () {
		　　　const res = uni.getSystemInfoSync();   //获取手机可使用窗口高度     api为获取系统信息同步接口
			 console.log(res.windowHeight)
		　　　this.style.pageHeight = res.windowHeight;
		　　　this.style.contentViewHeight = res.windowHeight - uni.getSystemInfoSync().screenWidth / 750 * (100) - 70; //像素   因为给出的是像素高度 然后我们用的是upx  所以换算一下 
		　},　　
		onLoad(res) {
			
			this.uid = res.uid
			this.fid = res.fid
			uni.setNavigationBarTitle({
			　　title: res.title
			})
			this.getMsg()
		},
		mounted() {
			this.scrollToBottom();
		},
		methods: {
			sendVideo() {
				this.scrollToBottom()
				let reg = /^(?!(\s+$))/ //不能全是空格
				if (1) {
					this.scrollAnimation = true
					const a = {
						id: this.uid,
						fid: this.fid,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: 'https://img.cdn.aliyun.dcloud.net.cn/guide/uniapp/%E7%AC%AC1%E8%AE%B2%EF%BC%88uni-app%E4%BA%A7%E5%93%81%E4%BB%8B%E7%BB%8D%EF%BC%89-%20DCloud%E5%AE%98%E6%96%B9%E8%A7%86%E9%A2%91%E6%95%99%E7%A8%8B@20181126-lite.m4v',
						neir: "",
						sendTime: this.getTime()
					}
					this.chat.push(a);
					// 发送信息到socket
					this.socket.emit('msg', a)
					this.$nextTick(function(){
						// this.scrollAnimation = true
						this.scrollToBottom();   //创建后调用回到底部方法
					})
					this.showSendBtn = false
				}
			},
			getTime:function(){
			var date = new Date(),
			year = date.getFullYear(),
			month = date.getMonth() + 1,
			day = date.getDate(),
			hour = date.getHours() < 10 ? "0" + date.getHours() : date.getHours(),
			minute = date.getMinutes() < 10 ? "0" + date.getMinutes() : date.getMinutes(),
			second = date.getSeconds() < 10 ? "0" + date.getSeconds() : date.getSeconds();
			month >= 1 && month <= 9 ? (month = "0" + month) : "";
			day >= 0 && day <= 9 ? (day = "0" + day) : "";
			// var timer = year + '-' + month + '-' + day + ' ' + hour + ':' + minute + ':' + second;
			var timer = hour + ':' + minute;
			return timer;
			},
			sendChange (){
				let reg = /^(?!(\s+$))/ //不能全是空格
				if (this.chatm.length > 0 && reg.test(this.chatm)) {
					this.showSendBtn = true
				} else {
					this.showSendBtn = false
				}
			},
			scrollToBottom () {
			            let that = this;
			            let query = uni.createSelectorQuery();
			            query.selectAll('.m-item').boundingClientRect();
			            query.select('#scrollview').boundingClientRect();
			            query.exec((res) => {
			                that.style.mitemHeight = 0;
			                res[0].forEach((rect) => that.style.mitemHeight = that.style.mitemHeight + rect.height + 40)   //获取所有内部子元素的高度
			　　　　　　　　　　 // 因为vue的虚拟DOM 每次生成的新消息都是之前的，所以采用异步setTimeout    主要就是添加了这红字
			　　　　　　　　　　 setTimeout(() => {
			                　　if (that.style.mitemHeight > (that.style.contentViewHeight - 100)) {   //判断子元素高度是否大于显示高度
			                    　　that.scrollTop = that.style.mitemHeight - that.style.contentViewHeight    //用子元素的高度减去显示的高度就获益获得序言滚动的高度
			                　　}
			　　　　　　　　　}, 100)
			　　　　　　　})
			        },
			sendMsg () {
				this.scrollToBottom()
				let reg = /^(?!(\s+$))/ //不能全是空格
				if (this.chatm.length > 0 && reg.test(this.chatm)) {
					this.scrollAnimation = true
					const a = {
						id: this.uid,
						fid: this.fid,
						img: '../../static/feicheng.png',
						name: '飞橙',
						video: '',
						neir: this.chatm,
						sendTime: this.getTime()
					}
					this.chat.push(a);
					// 发送信息到socket
					this.socket.emit('msg', a)
					this.$nextTick(function(){
						// this.scrollAnimation = true
						this.scrollToBottom();   //创建后调用回到底部方法
					})
					this.showSendBtn = false
					this.chatm = '';
				}
			},
			getMsg () {
				// 接收广播的信息
				this.socket.on('gbmsg', data => {
					this.chat.push(data);
					this.$nextTick(function(){
						// this.scrollAnimation = true
						this.scrollToBottom();   //创建后调用回到底部方法
					})
				})
			}
		}	
	}
</script>

<style lang="scss">
	page{
		background-color: #f5f5f5;
	}
		.main{
			.msg{
				display: flex;
				align-items:flex-end;
				padding: 50rpx 0;
				image{
					flex: none;
					background-color: #FFFFFF;
					width:80rpx;
					height:80rpx;
					border-radius:18rpx;
					margin: 0 20rpx;
					
				}
				.nr{
					.neir{
						display: block;
						max-width:420rpx;
						padding:20rpx 28rpx;
						min-height:40rpx;
						font-size:30rpx;
						color:rgba(25,29,35,1);
						line-height:40rpx;
						word-break: break-all;
						word-wrap: break-word;
						.imgc{
							width: 200rpx;
							height: 200rpx;
						}
					}
					.nt{
						padding-top: 8rpx;
						position: absolute;
						font-size:24rpx;
						color:rgba(25,29,35,0.5);
						line-height:34rpx;
					}
				}
			}
			.left{
				flex-direction: row;
				.neir{
					background: #FFFFFF;
					border-radius:24rpx 24rpx 24rpx 0px;
				}
			}
			.right{
				flex-direction: row-reverse;
				.neir{
					background:rgba(255,234,222,1);
					border-radius:24rpx 24rpx 0px 24rpx;
				}
				.nt{
					right: 132rpx;
				}
			}
			.center{
				text-align: center;
				padding: 32rpx 0 20rpx;
				.inner{
					font-size:24rpx;
					display: inline-block;
					color:rgba(25,29,35,0.8);
					line-height:34rpx;
				}
			}
		}
		.send{
				position: fixed;
				z-index: 1002;
				bottom: 0;
				width: 100%;
				min-height: 70rpx;
				background:rgba(255,255,255,0.96); 	
				display: flex;
				.chat-send{
					margin: 16rpx 160rpx 16rpx 70rpx;
					flex: 1;
					width: 100%;
					min-height:52rpx;
					background:rgba(242,242,242,1);
					border-radius:18rpx;
					font-size:28rpx;
					color:rgba(25,29,35,1);
					line-height:52rpx;
					padding: 10rpx 18rpx;
					word-break: break-all;
					word-wrap: break-word;
				}
				.mic-icon,.plus-icon,.smile-icon {
					width: 30rpx;
					height: 30rpx;
					position: absolute;
				}
				.mic-icon {
					left: 10rpx;
					top: 20rpx;
				}
				.plus-icon {
					right: 50rpx;
					top: 22rpx;
				}
				.smile-icon{
					right: 116rpx;
					top: 22rpx;
				}
				.send-icon{
					height: 48rpx;
					line-height: 48rpx;
					font-size: 24rpx;
					position: absolute;
					right: 12rpx;
					top: 24rpx;
					color: #FFFFFF;
					padding: 0  14rpx!important;
					background-color: #07c160;
					
				}
				// image{
				// 	width: 48rpx;
				// 	height: 48rpx;
				// 	position: absolute;
				// 	right: 68rpx;
				// 	top: 32rpx;
				// }
			}
</style>
