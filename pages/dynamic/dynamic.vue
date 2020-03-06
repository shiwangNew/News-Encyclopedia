<template>
	<view class="dynamic">
		<!-- 导航栏 -->
		<dynamic-tabs :tabBars='tabBars' :currentTab='currentTab' @changeTabIndex='changeTabIndex'></dynamic-tabs>
		<!-- 内容 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperHeight+'px'}" @change='changeSwiper' :current="tabIndex">
				<swiper-item>
					<scroll-view scroll-y="true" class="scroll-v list" @scrolltolower="loadMore()">
						<view class="focus">
							<block v-for="(item,index) in guanzhu.list" :key='index'>
								<common-list :item='item' :index='index' @changeFocus = 'changeFollow'></common-list>
							</block>
						</view>
						<!-- 加载更多 -->
						<load-more :loadtext="guanzhu.loadtext"></load-more>
					</scroll-view>
				</swiper-item>
				<swiper-item>
					<scroll-view scroll-y="true" class="scroll-v list" @scrolltolower="loadMore()">
						<view class="topic-input">
							<input class="uni-input" placeholder="搜索内容" placeholder-class="icon iconfont icon-sousuo" />
						</view>
						<view class="rotationChart">
							<swiper :indicator-dots="true" :autoplay="true" :interval="3000" :duration="1000">
								<swiper-item v-for="(item,index) in topic.swiper" :key='index'>
									<image :src="item.src" mode="widthFix" lazy-load></image>
								</swiper-item>
							</swiper>
						</view>
						<!-- 热门分类 -->
						<dynamic-classification :nav = 'topic.nav'></dynamic-classification>
						<!-- 最近更新 -->
						<view class="lately-update">
							<view class="title">
								最近更新
							</view>
							<block v-for="(item,index) in topic.list" :key='index'>
								<dynamic-update :item='item' :index='index'></dynamic-update>
							</block>
						</view>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import dynamicTabs from '../../components/dynamic/dynamic-tabs.vue'
	import commonList from '../../components/common/common-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	import dynamicClassification from '../../components/dynamic/dynamic-classification.vue'
	import dynamicUpdate from '../../components/dynamic/dynamic-update.vue'
	export default {
		data() {
			return {
				// swiper索引
				tabIndex:0,
				// swiper的高度
				swiperHeight:500,
				// 导航栏数据
				tabBars:[
					{name:"关注",id:"guanzhu"},
					{name:"话题",id:"topic"}
				],
				// 当前导航栏的索引
				currentTab:'0',
				// 列表数据
				guanzhu:{
					loadtext:"上拉加载更多",
					list:[
						// 文字
						{
							userpic:"../../static/demo/userpic/12.jpg",
							username:"哈哈",
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
							sex:1, //0 男 1 女
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
							username:"哈哈",
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
						// 分享
						{
							userpic:"../../static/demo/userpic/12.jpg",
							username:"哈哈",
							sex:0, //0 男 1 女
							age:25,
							isguanzhu:false,
							title:"我是标题",
							titlepic:"",
							video:false,
							share:{
								title:"我是分享的标题",
								titlepic:"../../static/demo/datapic/14.jpg"
							},
							path:"深圳 龙岗",
							sharenum:20,
							commentnum:30,
							goodnum:20
						},
					]
				},
				// 轮播图片
				topic:{
					swiper:[
						{ src:"../../static/demo/banner2.jpg" },
						{ src:"../../static/demo/banner2.jpg" },
						{ src:"../../static/demo/banner2.jpg" },
					],
					nav:[
						{name:"最新"},
						{name:"游戏"},
						{name:"打卡"},
						{name:"情感"},
						{name:"故事"},
						{name:"喜爱"},
					],
					list:[
						{
							titlepic:"../../static/demo/topicpic/13.jpeg",
							title:"话题名称",
							desc:"我是话题描述",
							totalnum:50,
							todaynum:10
						},
						{
							titlepic:"../../static/demo/topicpic/13.jpeg",
							title:"话题名称",
							desc:"我是话题描述",
							totalnum:50,
							todaynum:10
						},
						{
							titlepic:"../../static/demo/topicpic/13.jpeg",
							title:"话题名称",
							desc:"我是话题描述",
							totalnum:50,
							todaynum:10
						},
						{
							titlepic:"../../static/demo/topicpic/13.jpeg",
							title:"话题名称",
							desc:"我是话题描述",
							totalnum:50,
							todaynum:10
						},
						{
							titlepic:"../../static/demo/topicpic/13.jpeg",
							title:"话题名称",
							desc:"我是话题描述",
							totalnum:50,
							todaynum:10
						},
						{
							titlepic:"../../static/demo/topicpic/13.jpeg",
							title:"话题名称",
							desc:"我是话题描述",
							totalnum:50,
							todaynum:10
						}
					]
				}
			};
		},
		components:{
			dynamicTabs,
			commonList,
			loadMore,
			dynamicClassification,
			dynamicUpdate
		},
		onLoad(){
			uni.getSystemInfo({
			    success:  (res) => {
					// 获取swiperHeight可以获取的高度，窗口高度减去导航栏高度
					this.swiperHeight = res.windowHeight - uni.upx2px(90)
					// console.log(this.swiperHeight)
			    }
			});
		},
		methods:{
			changeTabIndex(index){
				// console.log(index)
				this.tabIndex = index
			},
			// 关注
			changeFollow(index){
				this.guanzhu.list[index].isguanzhu = true
				uni.showToast({
					title:'关注成功'
				})
			},
			changeSwiper(e){
				// console.log(e.detail.current)
				this.currentTab = e.detail.current
			},
			// 上拉加载
			loadMore(){
				if(this.guanzhu.loadtext != '上拉加载更多'){
					return
				}
				let obj = {
					userpic:"../../static/demo/userpic/12.jpg",
					username:"哈哈",
					sex:0, //0 男 1 女
					age:25,
					isguanzhu:false,
					title:"我是标题",
					titlepic:"",
					video:false,
					share:{
						title:"我是分享的标题",
						titlepic:"../../static/demo/datapic/14.jpg"
					},
					path:"深圳 龙岗",
					sharenum:20,
					commentnum:30,
					goodnum:20
				};
				this.guanzhu.loadtext = '加载中'
				this.guanzhu.list.push(obj)
				setTimeout(()=>{
					this.guanzhu.loadtext = '上拉加载更多'
				},100)
			},
		}
	}
</script>

<style lang="scss" scoped>
	.dynamic{
		.uni-navbar{
			border-bottom: 1upx solid #C8C7CC;
		}
		.focus{
			padding: 18upx;
		}
		.topic-input{
			padding: 20upx;
			font-size: 12upx;
			text-align: center;
			input{
				border-radius: 10upx;
				background-color: #f5f5f5;
			}
			.iconfont{
				font-size: 28upx;
				color: #A0A0A0;
			}
		};
		.rotationChart{
			padding: 0 20upx 20upx 20upx;
			image{
				width: 100%;
				border-radius: 10upx;
			}
		};
		.lately-update{
			padding: 20upx;
			.title{
				color: #2F2F2F;
				margin-bottom: 20upx;
			}
		}
	}
	.uni-navbar__header{
		height: 180upx !important;
	}
</style>
