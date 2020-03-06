<template>
	<view>
		<!-- 热门分类 -->
		<view class="classification">
			<view class="classification-top">
				<view class="title">
					热门分类
				</view>
				<view class="more" @tap='toMore()'>
					<text>
						更多
						<text class="icon iconfont icon-youjiantou"></text>
					</text>
				</view>
			</view>
			<view class="classification-bottom">
				<view class="term" v-for="(item,index) in nav" :key='index'>
					{{item.name}}
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
			nav:Array
		},
		methods:{
			toMore(){
				uni.navigateTo({
					url:'../../pages/topic-type/topic-type'
				})
			}
		}
	}
</script>

<style lang="scss" scoped>
	.classification{
		border-top: 1upx solid #D6D6D6;
		border-bottom: 1upx solid #D6D6D6;
		padding: 20upx;
		font-size: 32upx;
		.classification-top{
			display: flex;
			.title{
				flex: 1;
				color: #616161;
			};
			.more{
				flex: 1;
				text-align: right;
				color: #D6D6D6;
			}
		};
		.classification-bottom{
			display: flex;
			margin-top: 20upx;
			.term{
				text-align: center;
				flex: 1;
				padding: 8upx 12upx;
				background-color: #F7F7F7;
				margin-right: 20upx;
				color: #A2A2A2;
				&:nth-child(6){
					margin-right: 0upx;
				}
			}
		}
	};
</style>
