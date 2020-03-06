<template>
	<view class="topic-detail">
		<!-- 背景虚化图 -->
		<view class="detail-bg">
			<image src="../../static/demo/topicpic/13.jpeg" mode="aspectFill" lazy-load></image>
		</view>
		<!-- 头像、描述 -->
		<detail-mess-info :topicInfo='topicInfo'></detail-mess-info>
		<!-- 导航栏 -->
		<tabs :currentIndex="currentIndex" @returnDate='returnDate' :tabBars="tabBars" scrollStyle='border-bottom:none' scrollItemStyle='width:50%'></tabs>
		<!-- 数据展示 -->
		<view class="show-info">
			<block v-for="(item,index) in tablist" :key='index'>
				<template v-if="currentIndex == index">
					<block v-for="(item1,index1) in item.list" :key='index1'>
						<common-list :item='item1' :index='index1' @changeFocus = 'changeFollow'></common-list>
					</block>
					<load-more :loadtext="item.loadtext"></load-more>
				</template>
			</block>
		</view>
	</view>
</template>

<script>
	import detailMessInfo from '../../components/topic-detail/detail-mess-info.vue';
	import tabs from '../../components/home/home-tabs.vue'
	import commonList from '../../components/common/common-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	export default {
		data() {
			return {
				topicInfo:{
					titlepic:"../../static/demo/topicpic/13.jpeg",
					title:"忆往事，敬余生",
					desc:"我是描述",
					totalnum:1000,
					todaynum:1000,
				},
				tabBars:[
					{ name:"默认",id:"moren" },
					{ name:"最新",id:"zuixin" }
				],	
				// 当前索引
				currentIndex:0,
				// 列表数据
				tablist:[
					{
						loadtext:"上拉加载更多",
						list:[
							// 文字
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈111",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 图文
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈111",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 视频
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈111",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:{
									looknum:"20w",
									long:"2:47"
								},
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							// 文字
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈222",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 图文
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈222",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:false,
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
							// 视频
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"哈哈222",
								sex:0, //0 男 1 女
								age:25,
								isguanzhu:false,
								title:"我是标题",
								titlepic:"../../static/demo/datapic/13.jpg",
								video:{
									looknum:"20w",
									long:"2:47"
								},
								share:false,
								path:"深圳 龙岗",
								sharenum:20,
								commentnum:30,
								goodnum:20
							},
						]
					},
				]
			};
		},
		components:{
			detailMessInfo,
			tabs,
			commonList,
			loadMore
		},
		// 上拉加载
		onReachBottom(){
			this.loadMore(this.currentIndex)
		},
		// 监听下拉刷新事件
		onPullDownRefresh(){
			this.getData()
		},
		methods:{
			// 关闭下拉刷新
			getData(){
				let obj = {
					userpic:"../../static/demo/userpic/12.jpg",
					username:"哈哈999",
					sex:0, //0 男 1 女
					age:25,
					isguanzhu:false,
					title:"我是标题",
					titlepic:"",
					video:false,
					share:false,
					path:"深圳 龙岗",
					sharenum:20,
					commentnum:30,
					goodnum:20
				}
				this.tablist[this.currentIndex].list.unshift(obj)
				setTimeout(()=>{
					uni.stopPullDownRefresh();
				},2000)
			},
			returnDate(e){
				// console.log(e)
				this.tabIndex = e
				this.currentIndex = e
			},
			// 关注
			changeFollow(index){
				this.guanzhu.list[index].isguanzhu = true
				uni.showToast({
					title:'关注成功'
				})
			},
			// 上拉加载数据
			loadMore(index){
				// console.log(index)
				if(this.tablist[index].loadtext != '上拉加载更多'){
					return
				}
				let obj = {
					userpic:"../../static/demo/userpic/12.jpg",
					username:"哈哈111",
					sex:0, //0 男 1 女
					age:25,
					isguanzhu:false,
					title:"我是标题",
					titlepic:"",
					video:false,
					share:false,
					path:"深圳 龙岗",
					sharenum:20,
					commentnum:30,
					goodnum:20
				}
				this.tablist[index].loadtext = '加载中'
				this.tablist[index].list.push(obj)
				setTimeout(()=>{
					this.tablist[index].loadtext = '上拉加载更多'
				},100)
			},
		}
	}
</script>

<style lang="scss">
	.topic-detail{
		.detail-bg{
			width: 100%;
			height: 300upx;
			position: relative;
			overflow: hidden;
			image{
				position: absolute;
				width: 100%;
				filter: blur(10px);
			}
		};
		.show-info{
			padding: 20upx;
		}
	}
</style>
