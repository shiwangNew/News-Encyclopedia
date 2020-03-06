<template>
	<view class="user-list">
		<!-- 导航栏 -->
		<tabs :currentIndex="currentIndex" @returnDate='returnDate' :tabBars="tabBars" scrollStyle='border-bottom:none' scrollItemStyle='width:33.3%'></tabs>
		<!-- 互相关注 -->
		<view class="uni-tab-bar">
			<swiper class="swiper-box" :style="{height:swiperHeight+'px'}" @change='changeSwiper' :current="tabIndex">
				<swiper-item class="swiper-item" v-for="(items,index) in newslist" :key="index">
					<scroll-view scroll-y="true" class="scroll-v list" @scrolltolower="loadMore(index)">
						<template v-if="items.list.length>0">
							<!-- 图文列表 -->
							<block v-for="(item1,index1) in items.list" :key="index1">
								<user-list :item1='item1' :index1='index1'></user-list>
							</block>
							<!-- 上拉加载 -->
							<load-more :loadtext="items.loadtext"></load-more>
						</template>
					</scroll-view>
				</swiper-item>
			</swiper>
		</view>
	</view>
</template>

<script>
	import tabs from '../../components/home/home-tabs.vue'
	import userList from '../../components/user-list/user-list.vue'
	import loadMore from '../../components/common/load-more.vue'
	export default {
		data() {
			return {
				tabIndex:0,
				// 当前索引
				currentIndex:0,
				// swiper的高度
				swiperHeight:500,
				tabBars:[
					{ name:"互关",id:"huguan",num:10 },
					{ name:"关注",id:"guanzhu",num:20 },
					{ name:"粉丝",id:"fensi",num:30 },
				],
				newslist:[
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							}
						]
					},
					{
						loadtext:"上拉加载更多",
						list:[
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:20,
								sex:0,
								isguanzhu:true
							},
							{
								userpic:"../../static/demo/userpic/11.jpg",
								username:"昵称",
								age:21,
								sex:1,
								isguanzhu:false
							}
						]
					}
				]
			};
		},
		components:{
			tabs,
			userList,
			loadMore
		},
		// 监听点击导航栏事件
		onNavigationBarButtonTap(e){
			if(e.index == 0){
				uni.navigateBack({
					delta:1
				})
			}
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
			returnDate(e){
				// console.log(e)
				this.tabIndex = e
				this.currentIndex = e
			},
			changeSwiper(e){
				// console.log(e.detail.current)
				this.currentIndex = e.detail.current
			},
			// 上拉加载事件
			loadMore(index){
				// console.log(index)
				if(this.newslist[index].loadtext != '上拉加载更多'){
					return
				}
				let obj = {
					userpic:"../../static/demo/userpic/11.jpg",
					username:"昵称",
					age:20,
					sex:0,
					isguanzhu:true
				}
				this.newslist[index].loadtext = '加载中'
				this.newslist[index].list.push(obj)
				setTimeout(()=>{
					this.newslist[index].loadtext = '上拉加载更多'
				},100)
			},
		}
	}
</script>

<style lang="scss" scoped>
	.user-list{
		.uni-tab-bar{
			
		}
	}
</style>
