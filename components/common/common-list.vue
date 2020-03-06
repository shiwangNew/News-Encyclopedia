<template>
	<view class="focuson-list">
		<view class="focuson-list-ava">
			<image :src="item.userpic" mode="widthFix"></image>
		</view>
		<view class="focuson-list-content">
			<view class="content-one">
				<view class="content-one-left">
					<text class="name">{{item.username}}</text>
					<sex-age :age='item.age' :sex='item.sex'></sex-age>
				</view>
				<view class="content-one-right">
					<text class="icon iconfont icon-jiahao" v-show="!item.isguanzhu" @tap="changeFollow(index)"><text></text>关注</text>
					<text class="icon iconfont icon-error"></text>
				</view>
			</view>
			<view class="content-two">
				<text>{{item.title}}</text>
			</view>
			<view class="content-three">
				<image v-if="item.titlepic" :src="item.titlepic" mode="widthFix" lazy-load></image>
				<view class="isPlayed" v-if="item.video">
					<text class="icon iconfont icon-bofang"></text>
					<view class="played">
						<view>{{item.video.looknum}} 次播放 {{item.video.long}}</view>
					</view>
				</view>
				<!-- 分享 -->
				<view class="three-share" v-if="item.share">
					<view class="share-image">
						<image :src="item.share.titlepic" mode="widthFix" lazy-load></image>
					</view>
					<view class="share-desc">
						<text>{{item.share.title}}</text>
					</view>
				</view>
			</view>
			<view class="content-four">
				<view class="content-four-left">
					<text>{{item.path}}</text>
				</view>
				<view class="content-four-right">
					<text class="marginR"><text class="icon iconfont icon-zhuanfa"></text>{{item.sharenum}}</text>
					<text class="marginR"><text class="icon iconfont icon-duanxin"></text>{{item.commentnum}}</text>
					<text><text class="icon iconfont icon-iconzhengli_dianzan"></text>{{item.goodnum}}</text>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import sexAge from './sex-age.vue'
	export default {
		data() {
			return {
				
			};
		},
		components:{
			sexAge
		},
		props:{
			item:Object,
			index:Number
		},
		methods:{
			changeFollow(index){
				this.$emit('changeFocus',index)
			}
		}
	}
</script>

<style lang="scss">
	.focuson-list{
		display: flex;
		margin-top: 10upx;
		.focuson-list-ava{
			width: 130upx;
			image{
				width: 100upx;
				height: 100upx;
				border-radius: 50%;
			}
		};
		.focuson-list-content{
			padding-left: 16upx;
			flex: 1;
			border-bottom: 1upx solid #C8C7CC;
			&:last-child{
				border-bottom: none;
			}
			.content-one{
				display: flex;
				.content-one-left{
					flex: 1;
					.name{
						font-size: 32upx;
						color: #A8A8A8;
						margin-right: 8upx;
						display: inline-block;
					}
					
				}
				.content-one-right{
					flex: 1;
					text-align: right;
					.icon-jiahao{
						background-color: #F4F4F4;
						padding: 8upx;
						border-radius: 6upx;
						margin-right: 10upx;
						text{
							margin-left: 10upx;
						}
						font-size: 30upx;
					}
					.icon-error{
						color: #D5D5D5;
						font-size: 34upx;
					}
				}
			}
			.content-two{
				color: #343434;
				font-size: 36upx;
			};
			.content-three{
				margin-top: 10upx;
				image{
					width: 100%;
				};
				.isPlayed{
					position: relative;
					height: 100%;
					.icon-bofang{
						font-size: 130upx;
						position: absolute;
						top: 50%;
						left: 50%;
						color: #FFFFFF;
						transform: translate(-50%,-125%);
					};
					.played{
						// display: inline-block;
						position: absolute;
						bottom: 20upx;
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
				.three-share{
					display: flex;
					padding: 16upx 10upx;
					background-color: #F7F7F7;
					border-radius: 16upx;
					.share-image{
						flex: 1;
						image{
							width: 100%;
							overflow: hidden;
							border-radius: 10upx;
						}
						margin-right: 15upx;
					};
					.share-desc{
						flex: 3;
						color: #3A3A3A;
						font-size: 24upx;
					}
				}
			};
			.content-four{
				display: flex;
				.content-four-left{
					flex: 1;
					color: #BCBCBC;
					text{
						margin-right: 10upx;
					}
				};
				.content-four-right{
					flex: 1;
					text-align: right;
					color: #BCBCBC;
					.marginR{
						margin-right: 10upx;
					} 
					.iconfont{
						margin-right: 5upx;
						font-size: 30upx;
					}
				}
			}
		}
	}
</style>
