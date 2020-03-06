<template>
	<view>
		<view class="update-list" @tap='toTopicDetail()'>
			<view class="listPic">
				<image :src="item.titlepic" mode="widthFix" lazy-load></image>
			</view>
			<view class="list-info">
				<view class="list-info-title">
					#{{item.title}}#
				</view>
				<view class="list-info-mess">
					{{item.desc}}
				</view>
				<view class="list-info-mess">
					动态 {{item.totalnum}}
					今日 {{item.todaynum}}
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
			toTopicDetail(){
				uni.navigateTo({
					url:'../../pages/topic-detail/topic-detail'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.update-list{
		display: flex;
		border-bottom: 1upx solid #D6D6D6;
		padding: 20upx 0upx;
		&:last-child{
			border-bottom: none;
		}
		.listPic{
			flex: 1;
			image{
				width: 100%;
				border-radius: 12upx;
			}
		};
		.list-info{
			flex: 3;
			padding-left: 20upx;
			font-size: 20upx;
			.list-info-title{
				
			}
			.list-info-mess{
				color: #9A9A9A;
			}
		}
	}
</style>
