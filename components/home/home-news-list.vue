<template>
 	<view class="block" animated fadeIn fast>
 		<view class="news_list" v-if="item">
 			<view class="news_list_item1">
 				<view>
 					<image :src=item.userpic mode="aspectFit" lazy-load class="userImg"></image>
 					<text>{{item.username}}</text>
 				</view>
 				<view>
 					<view v-show="!item.isguanzhu" @tap="focusOn">
 						<text><text class="icon iconfont icon-jiahao"></text>关注</text>
 					</view>
 					<text class="icon iconfont icon-error"></text>
 				</view>
 			</view>
 			<view class="news_list_item2">
 				<text>{{item.title}}</text>
 			</view>
 			<view class="news_list_item3">
 				<image :src="item.titlepic" mode="aspectFit" lazy-load></image>
 				<view class="isPlayed" v-if="item.type === 'video' ">
 					<text class="icon iconfont icon-bofang"></text>
 					<view class="played">
 						<view>{{item.playnum}} 次播放 {{item.long}}</view>
 					</view>
 				</view>
 			</view>
 			<view class="news_list_item4">
 				<view>
 					<text @tap="giveLike(item)"><text class="icon iconfont icon-xiaolian" :class="{'active':(item.infonum.index==1)}"></text>{{item.infonum.dingnum}}</text>
 					<text @tap="cancelPraise"><text class="icon iconfont icon-bukaixin" :class="{'active':(item.infonum.index==2)}"></text>{{item.infonum.cainum}}</text>
 				</view>
 				<view>
 					<text><text class="icon iconfont icon-duanxin"></text>{{item.commentnum}}</text>
 					<text><text class="icon iconfont icon-zhuanfa"></text>{{item.sharenum}}</text>
 				</view>
 			</view>
 		</view>
 	</view>
 </template>
 
 
 
<script>
	export default {
		data() {
			return {
				
			};
		},
		props:{
			item:Object,
			index:Number
		},
		methods:{
			// 点击关注
			focusOn(){
				this.item.isguanzhu = true
				uni.showToast({
				    title: '关注成功',
				});
			},
			// 点赞
			giveLike(item){
				if(this.item.infonum.index==1){ return; }
				this.item.infonum.dingnum++;
				if(this.item.infonum.index==2){
					this.item.infonum.cainum--;
				}
				this.item.infonum.index=1;
			},
			// 取消赞
			cancelPraise(){
				if(this.item.infonum.index==2){ return; }
				this.item.infonum.cainum++;
				if(this.item.infonum.index==1){
					this.item.infonum.dingnum--;
				}
				this.item.infonum.index=2;
			}
		}
	}
</script>

<style lang="scss" scoped>
	.block{
		.news_list{
			padding: 0 16upx;
			margin: 20upx 0;
			padding-bottom: 10upx;
			border-bottom: 1rpx solid #ccc;
			.news_list_item1{
				display: flex;
				justify-content: space-between;
				align-items: center;
				view{
					&:nth-child(1){
						.userImg{
							width: 92upx;
							height: 92upx;
							border-radius: 50%;
							vertical-align: middle;
							margin-right: 20upx;
						}
						text{
							color: #B2B2B2;
							font-size: 30upx;
						}
					},
					&:nth-child(2){
						view{
							display:inline-block;
							padding: 6upx 10upx;
							background-color: #F4F4F4;
							margin-right: 14upx;
						}
					}
				}
				
			};
			.news_list_item2{
				margin-top: 18upx;
				text{
					font-size: 30upx;
					font-weight: 700;
				}
			};
			.news_list_item3{
				margin-top: 18upx;
				width: 100%;
				height: 400upx;
				position: relative;
				image{
					width: 100%;
					height: 100%;
					border-radius: 10upx;
					padding: 0;
					margin: 0;
				};
				text{
					position: absolute;
					top: 50%;
					left: 50%;
					transform: translate(-50%,-50%);
					font-size: 180upx;
					color: #fff;
				};
				.played{
					// display: inline-block;
					position: absolute;
					bottom: 14upx;
					right: 8upx;
					view{
						font-size: 20upx;
						color: #fff;
						padding: 12upx;
						background-color: rgba(0,0,0,0.4);
						border-radius: 36upx;
					}
				}
			};
			.news_list_item4{
				margin-top: 10upx;
				display: flex;
				justify-content: space-between;
				align-items: center;
				color: #D5D5D5;
				view{
					text{
						margin-right: 10upx;
						.active{
							color: #4CD964;
						}
					}
				}
			}
		}
	}
</style>
