<template>
	<view class="chat-list">
		<uni-list>
		    <uni-list :border="true">
		        <!-- 自定义右侧内容 -->
		        <uni-list-chat link="navigateTo" v-for="(item, index) in avatarList" :key="index" @click="toChat(item)" :title="item.userName" :avatar="item.avatarImg" :note="item.note" :time="item.time" badge-positon="left" :badge-text="item.textDot">
		            <view class="chat-custom-right">
		                <text class="chat-custom-text">{{item.lastSentTime}}</text>
		                <!-- 需要使用 uni-icons 请自行引入 -->
		                <uni-icons :type="item.icons" color="#999" size="16"></uni-icons>
		            </view>
		        </uni-list-chat>
		    </uni-list>
		</uni-list>
	</view>
</template>

<script>
	export default {
		components: {
		           
		        },
		data() {
			return {
				avatarList: [
					{
						uid: 2,
						fid: 3,
						userName: '飞橙科技',
						avatarImg: '../../static/feicheng.png',
						note: '您收到一条新的消息您收到一条新的消息您收到一条新的消息',
						time: '2020-02-02',
						textDot: '99+',
						lastSentTime: '17:48',
						icons: 'weixin'
					},
					{
						uid: 1,
						fid:4,
						userName: '飞橙科技飞橙科技飞橙科技飞橙科技',
						avatarImg: '../../static/feicheng.png',
						note: '您收到一条新的消息您收到一条新的消息您收到一条新的消息',
						time: '2020-02-02',
						textDot: '99',
						lastSentTime: '周一',
						icons: 'star-filled'
					},
					{
						uid: 1,
						fid: 5,
						userName: '飞橙',
						avatarImg: '../../static/feicheng.png',
						note: '您收到一条新的消息您收到一条新的消息您收到一条新的消息',
						time: '2020-02-02',
						textDot: '9',
						lastSentTime: '2020-9-27',
						icons: 'false'
					},
					{
						uid: 1,
						fid: 6,
						userName: '飞橙直播',
						avatarImg: '../../static/feicheng.png',
						note: '您收到一条新的消息您收到一条新的消息您收到一条新的消息',
						time: '2020-02-02',
						textDot: 'dot',
						lastSentTime: '2020-9-27',
						icons: 'chat'
					}
				]
			}
		},
		onLoad() {
		},
		methods: {
		toChat(row) {
			uni.navigateTo({
				url: '../chatHome/chatHome?title=' + row.userName + '&uid=' + row.uid + '&fid=' + row.fid,
				success: res => {},
				fail: () => {},
				complete: () => {}
			})
		}
        }

	}
</script>

<style lang="scss">
	.chat-list{
		.chat-custom-right {
		    flex: 1;
		    /* #ifndef APP-NVUE */
		    display: flex;
		    /* #endif */
		    flex-direction: column;
		    justify-content: space-between;
		    align-items: flex-end;
		}
		
		.chat-custom-text {
		    font-size: 12px;
		    color: #999;
		}
		.uni-list--border-bottom {
			background-color: #FFFFFF!important;
		}
	}
</style>
