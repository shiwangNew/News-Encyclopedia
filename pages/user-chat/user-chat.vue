<template>
	<view class="user-chat">
		<!-- 聊天页 -->
		<scroll-view scroll-y :scroll-top="scrollTop" 
		:scroll-with-animation="true"
		:style="{height:style.contentH+'px'}">
			<block v-for="(item,index) in chatList" :key='index'>
				<view class="chat-item">
					<user-chat-talk :item='item' :index='index'></user-chat-talk>
				</view>
			</block>
		</scroll-view>
		<!-- 底部 -->
		<chat-bottom @submit='submitMess'></chat-bottom>
	</view>
</template>

<script>
	import chatBottom from '../../components/user-chat/user-chat-bottom.vue'
	import userChatTalk from '../../components/user-chat/user-chat-talk.vue'
	import time from '../../common/time.js'
	export default {
		data() {
			return {
				chatList:[
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:true,
						userpic:"../../static/demo/userpic/10.jpg",
						type:"img",
						data:"../../static/demo/3.jpg",
						time:"1555146414",
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:true,
						userpic:"../../static/demo/userpic/10.jpg",
						type:"img",
						data:"../../static/demo/3.jpg",
						time:"1555146414",
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:true,
						userpic:"../../static/demo/userpic/10.jpg",
						type:"img",
						data:"../../static/demo/3.jpg",
						time:"1555146414",
					},
					{
						isme:false,
						userpic:"../../static/demo/userpic/11.jpg",
						type:"text",
						data:"哈哈哈",
						time:"1555146412"
					},
					{
						isme:true,
						userpic:"../../static/demo/userpic/10.jpg",
						type:"img",
						data:"../../static/demo/3.jpg",
						time:"1555146414",
					},
				],
				newChatList:[],
				style:{
					contentH:0,
					itemH:0
				},
				scrollTop:0,
			};
		},
		components:{
			chatBottom,
			userChatTalk
		},
		onLoad(){
			this.initdata()
			this.changeTime()
			this.pageToBottom(true);
		},
		methods:{
			// 初始化参数
			initdata(){
				try {
					const res = uni.getSystemInfoSync();
					this.style.contentH=res.windowHeight - uni.upx2px(120);
				} catch (e) { }
			},
			// 更改时间戳
			changeTime(){
				for (let i = 0; i < this.chatList.length; i++) {
					this.chatList[i].gstime=time.gettime.getChatTime(this.chatList[i].time,i>0?this.chatList[i-1].time:0);
				}
				this.newChatList = this.chatList
				// console.log(this.newChatList)
			},
			// 提交内容
			submitMess(text){
				// console.log(text)
				let now=new Date().getTime();
				let obj={
					isme:true,
					userpic:"../../static/demo/userpic/10.jpg",
					type:"text",
					data:text,
					time:now,
					gstime:time.gettime.getChatTime(now,this.newChatList[this.newChatList.length-1].time)
				};
				this.newChatList.push(obj);
				this.pageToBottom();
			},
			pageToBottom(isfirst = false){
				let q=uni.createSelectorQuery().in(this);
				let itemH = q.selectAll('.chat-item');
				this.$nextTick(()=>{
					itemH.fields({
						size:true
					},data => {
						if (data) {
							if (isfirst) {
								for (let i = 0; i < data.length; i++) {
									this.style.itemH += data[i].height;
								}
							}else{
								this.style.itemH += data[data.length-1].height;
							}
							this.scrollTop = (this.style.itemH > this.style.contentH) ? this.style.itemH : 0;
						}
					}).exec();
				})
			},
		}
	}
</script>

<style lang="scss" scoped>
	.user-chat{
		padding: 20upx;
		
	}
</style>
