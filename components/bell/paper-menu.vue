<template>
	<view class="paper-menu" v-show="show">
		<view class="add-friend" @tap='addFriend'>
			<text class="icon iconfont icon-sousuo"></text>
			<text>加好友</text>
		</view>
		<view class="clear-mess" @tap='clearMess'>
			<text class="icon iconfont icon-sousuo"></text>
			<text>清除未读</text>
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
			show:Boolean
		}
	}
</script>

<style lang="scss" scoped>
	.paper-menu{
		width: 50%;
		padding: 20upx;
		position: fixed;
		margin-top: 10upx;
		right: 0;
		box-shadow: 1upx 1upx 20upx 2upx #CCCCCC;
		z-index: 2000;
		background-color: #FFFFFF;
		.add-friend{
			line-height: 70upx;
			font-size: 35upx;
			.icon{
				margin-right: 20upx;
			}
		};
		.clear-mess{
			line-height: 70upx;
			font-size: 35upx;
			.icon{
				margin-right: 20upx;
			}
		}
	}
</style>
