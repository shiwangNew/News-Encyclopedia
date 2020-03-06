<template>
	<view class="home">
		<!-- <tabs :currentIndex="currentIndex" @returnDate='returnDate'></tabs> -->
		<tabs :currentIndex="currentIndex" @returnDate='returnDate' :tabBars="tabBars" ></tabs>
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperHeight+'px'}" @change='changeSwiper' :current="tabIndex">
				<swiper-item class="swiper-item" v-for="(items,index) in newslist" :key="index">
					<scroll-view scroll-y="true" class="scroll-v list" @scrolltolower="loadMore(index)">
						
							<template v-if="items.list.length>0">
								<!-- 图文列表 -->
								<block v-for="(item,index1) in items.list" :key="index1">
									<news-List :item="item" :index="index1"></news-List>
								</block>
								<!-- 上拉加载 -->
								<load-more :loadtext="items.loadtext"></load-more>
							</template>
							<!-- 无内容 -->
							<template v-else>
								<no-thing></no-thing>
							</template>
						
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import newsList from '../../components/home/home-news-list.vue';
	import tabs from '../../components/home/home-tabs.vue'
	import loadMore from '../../components/common/load-more.vue'
	import noThing from '../../components/common/no-thing.vue'
	export default {
		data() {
			return {
				tabIndex:0,
				tabBars:[
					{ name:"关注",id:"guanzhu" },
					{ name:"推荐",id:"tuijian" },
					{ name:"体育",id:"tiyu" 	  },
					{ name:"热点",id:"redian"  },
					{ name:"财经",id:"caijing" },
					{ name:"娱乐",id:"yule"    },
				],	
				// swiper的高度
				swiperHeight:500,
				// 当前索引
				currentIndex:0,
				// 展示新闻数据
				newslist:[
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题1",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题11",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题2",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题22",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题3",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题33",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题4",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题44",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:false,
								title:"我是标题5",
								type:"img", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								infonum:{
									index:0,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							},
							{
								userpic:"../../static/demo/userpic/12.jpg",
								username:"昵称",
								isguanzhu:true,
								title:"我是标题55",
								type:"video", // img:图文,video:视频
								titlepic:"../../static/demo/datapic/11.jpg",
								playnum:"20w",
								long:"2:47",
								infonum:{
									index:1,//0:没有操作，1:顶,2:踩；
									dingnum:11,
									cainum:11,
								},
								commentnum:10,
								sharenum:10,
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[]
					},
					{
						loadtext:"上拉加载更多",
						list:[]
					},
					{
						loadtext:"上拉加载更多",
						list:[]
					}
				],
				
			};
		},
		components:{
			newsList,
			tabs,
			loadMore,
			noThing
		},
		onLoad(){
			uni.getSystemInfo({
			    success:  (res) => {
					// 获取swiperHeight可以获取的高度，窗口高度减去导航栏高度
					this.swiperHeight = res.windowHeight - uni.upx2px(80)
					// console.log(this.swiperHeight)
			    }
			});
		},
		onNavigationBarSearchInputClicked() {
			uni.navigateTo({
			    url: '../search/search'
			});
		},
		methods:{
			// 上拉加载数据
			loadMore(index){
				// console.log(index)
				if(this.newslist[index].loadtext != '上拉加载更多'){
					return
				}
				let obj = {
					userpic:"../../static/demo/userpic/12.jpg",
					username:"我是新增数据",
					isguanzhu:true,
					title:"我是新增数据55",
					type:"video", // img:图文,video:视频
					titlepic:"../../static/demo/datapic/13.jpg",
					playnum:"20w",
					long:"2:47",
					infonum:{
						index:1,//0:没有操作，1:顶,2:踩；
						dingnum:11,
						cainum:11,
					},
					commentnum:10,
					sharenum:10,
				}
				this.newslist[index].loadtext = '加载中'
				this.newslist[index].list.push(obj)
				setTimeout(()=>{
					this.newslist[index].loadtext = '上拉加载更多'
				},100)
			},
			changeSwiper(e){
				// console.log(e.detail.current)
				this.currentIndex = e.detail.current
			},
			returnDate(e){
				// console.log(e)
				this.tabIndex = e
				this.currentIndex = e
			},
			// 监听原生标题栏按钮点击事件
			onNavigationBarButtonTap(e){
				// console.log(e.index)
				switch (e.index){
					case 1:
						uni.navigateTo({
							url:'../add-news/add-news'
						})
						break;
					default:
						break;
				}
			}
		}
	}
</script>

<style lang="scss" scoped>
	.home{
		.uni-tab-bar{
			.swiper-box{
				.scroll-v{
					
				}
			}
		}
	}
</style>
