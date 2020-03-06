<template>
	<view class="detail-mess">
		<view class="detail-ava">
			<image :src="topicInfo.titlepic" mode="widthFix" lazy-load></image>
			<text>#{{topicInfo.title}}#</text>
		</view>
		<view class="dyna-num">
			<text>动态 {{topicInfo.totalnum}}</text>
			<text>今日 {{topicInfo.todaynum}}</text>
		</view>
		<view class="detail-topic">
			<text>{{topicInfo.desc}}</text>
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
			topicInfo:Object
		}
	}
</script>

<style lang="scss" scoped>
	.detail-mess{
		padding: 20upx;
		position: relative;
		top: -94upx;
		.detail-ava{
			image{
				width: 140upx;
				border-radius: 20upx;
			}
			text{
				font-size: 40upx;
				position: relative;
				top: -20upx;
				margin-left: 20upx;
			}
		};
		.dyna-num{
			color: #C9C9C9;
			text{
				&:nth-child(2){
					margin-left: 30upx;
				}
			}
		};
		.detail-topic{
			color: #9C9C9C;
			line-height: 40upx;
		}
	}
</style>
