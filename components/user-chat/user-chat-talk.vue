<template>
	<view class="user-chat-list">
		<view class="chat-time" v-if="item.gstime">
			{{item.gstime}}
		</view>
		<view :class="item.isme?'from-our':'from-other'">
			<view class="other-ava">
				<image :src="item.userpic" mode="widthFix" lazy-load></image>
			</view>
			<view class="chat-content">
				<view class="data" v-if="item.type =='text'">
					{{item.data}}
				</view>
				<view class="img" v-if="item.type =='img'">
					<image :src="item.data" mode=""></image>
				</view>
				<view class="arrow">
					
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
			item: Object,
			index: Number
		}
	}
</script>

<style lang="scss" scoped>
	.user-chat-list{
		.chat-time{
			padding: 40upx;
			text-align: center;
			color: #B9B9B9;
		};
		.from-other{
			display: flex;
			margin-bottom: 40upx;
			.other-ava{
				width: 100upx;
				image{
					width: 100upx;
					border-radius: 50%;
				}
			};
			.chat-content{
				flex: 1;
				margin-left: 40upx;
				margin-right: 130upx;
				background-color: #F4F4F4;
				border-radius: 20upx;
				padding: 30upx 20upx;
				position: relative;
				.arrow{
					position: absolute;
					width: 0upx;
					height: 0;
					top: 35upx;
					left: -37upx;
					border: solid 20upx;
					border-color: #fff #F4F4F4 #fff #fff;
				};
				image{
					max-width: 400upx;
				}
			}
		};
		.from-our{
			display: flex;
			margin-bottom: 40upx;
			flex-direction: row-reverse;
			.other-ava{
				width: 100upx;
				image{
					width: 100upx;
					border-radius: 50%;
				}
			};
			.chat-content{
				flex: 1;
				margin-right: 40upx;
				margin-left: 130upx;
				background-color: #F4F4F4;
				border-radius: 20upx;
				padding: 30upx 20upx;
				position: relative;
				.arrow{
					position: absolute;
					width: 0upx;
					height: 0;
					top: 35upx;
					right: -37upx;
					border: solid 20upx;
					border-color: #fff#fff #fff #F4F4F4 ;
				};
				image{
					max-width: 400upx;
				}
			}
		}
	}
</style>
