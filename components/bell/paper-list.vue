<template>
	<view class="paper-list" @tap='toMessDetail()'>
		<image :src="item.userpic" mode="widthFix" lazy-load></image>
		<view class="mess">
			<view class="mess-top">
				<view class="title">
					<text>{{item.username}}</text>
				</view>
				<view class="time">
					<text>{{item.time}}</text>
				</view>
			</view>
			<view class="mess-bottom">
				<view class="info">
					<text>{{item.data}}</text>
				</view>
				<view class="num">
					<uni-badge class="uni-badge-left-margin" :text="item.noreadnum" type="error" size="small"></uni-badge>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import uniBadge from '../uni-badge/uni-badge.vue'
	export default {
		data() {
			return {
				
			};
		},
		components:{
			uniBadge
		},
		props:{
			item:Object,
			index:Number
		},
		methods:{
			toMessDetail(){
				uni.navigateTo({
					url:'../../pages/user-chat/user-chat'
				})
			}
		}
	}
</script>

<style lang="scss">
	.paper-list{
		padding: 20upx 0;
		display: flex;
		border-bottom: 1upx solid #EFEFEF;
		&:last-child{
			border-bottom: none;
		}
		image{
			width: 100upx;
			border-radius: 50%;
		};
		.mess{
			flex: 1;
			padding-left: 20upx;
			.mess-top{
				display: flex;
				.title{
					flex: 1;
					font-size: 35upx;
					color: #000000;
					font-weight: 600;
				};
				.time{
					width: 80upx;
					color: #CDCDCD;
					text-align: right;
				}
			};
			.mess-bottom{
				display: flex;
				align-items: center;
				.info{
					flex: 1;
					color: #959595;
				};
				.num{
					width: 80upx;
				}
			}
			
		}
	}
</style>
