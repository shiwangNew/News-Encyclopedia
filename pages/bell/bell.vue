<template>
	<view class="paper">
		<!-- 小纸条 -->
		<!-- 遮罩 -->
		<view class="mask" v-show="show" @tap='closeMenu'>
			
		</view>
		<!-- 操作菜单 -->
		<paper-menu :show='show'></paper-menu>
		<!-- 消息列表 -->
		<block v-for="(item,index) in list" :key='index'>
			<paper-list :item='item' :index='index'></paper-list>
		</block>
		<load-more :loadtext="loadtext"></load-more>
	</view>
</template>

<script>
	import paperList from '../../components/bell/paper-list.vue';
	import loadMore from '../../components/common/load-more.vue'
	import paperMenu from '../../components/bell/paper-menu.vue'
	export default {
		data() {
			return {
				show:false,
				loadtext:"上拉加载更多",
				list:[
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:2
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:0
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:0
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:11
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:2
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:0
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:0
					},
					{
						userpic:"../../static/demo/userpic/12.jpg",
						username:"昵称",
						time:"10:21",
						data:"我是信息",
						noreadnum:11
					}
				]
			};
		},
		components:{
			paperList,
			loadMore,
			paperMenu
		},
		// 点击导航栏
		onNavigationBarButtonTap(e){
			// console.log(e)
			if(e.index == 1){
				this.openMenu()
			}else if(e.index == 0){
				uni.navigateTo({
					url:'../user-list/user-list'
				})
			}
		},
		// 页面上拉刷新
		onReachBottom(){
			this.loadMore()
		},
		// 页面下拉刷新
		onPullDownRefresh(){
			this.loadMoreTop()
		},
		methods:{
			// 上拉触底加载数据
			loadMore(){
				if(this.loadtext != '上拉加载更多'){
					return
				}
				let obj = {
					userpic:"../../static/demo/userpic/12.jpg",
					username:"昵称1111",
					time:"10:21",
					data:"我是信息",
					noreadnum:11
				}
				this.loadtext = '加载中'
				this.list.push(obj)
				setTimeout(()=>{
					this.loadtext = '上拉加载更多'
				},100)
			},
			// 页面下拉刷新
			loadMoreTop(){
				let obj = {
					userpic:"../../static/demo/userpic/12.jpg",
					username:"昵称2222",
					time:"10:21",
					data:"我是信息",
					noreadnum:11
				}
				this.list.unshift(obj)
				setTimeout(()=>{
					uni.stopPullDownRefresh()
				},2000)
			},
			// 打开、关闭菜单
			closeMenu(){
				this.show = false
			},
			openMenu(){
				this.show = true
			},
			// 加好友
			addFriend(){
				this.closeMenu()
			},
			clearMess(){
				this.closeMenu()
			}
		}
	}
</script>

<style lang="scss" scoped>
	.paper{
		padding: 0 20upx;
		position: relative;
		.mask{
			position: fixed;
			width: 100%;
			height: 100%;
			// left: 0;
			// right: 0;
			// bottom: 0;
			background-color: red;
			z-index: 1000;
			margin: 0 -20upx;
		};
	}
</style>
