<template>
	<view>
		<uni-nav-bar :statusBar="true" :fixed="true">
			<view class="left" slot='left'>
				<view class="nav-left">
					<text class="icon iconfont icon-qiandao"></text>
				</view>
			</view>
			<view class="nav-center">
				<view class="guanzhu" v-for="(item,index) in tabBars" :key='item.id' @tap="changeTab(index)">
					<text>{{item.name}}</text>
					<view class="nav-line" v-if="(currentTab == index)">
						
					</view>
				</view>
			</view>
			<view class="right" slot='right'>
				<view class="nav-right">
					<text class="icon iconfont icon-bianji"></text>
				</view>
			</view>
		</uni-nav-bar>
	</view>
</template>

<script>
	import uniNavBar from '../uni-nav-bar/uni-nav-bar.vue'
	export default {
		data() {
			return {
				
			};
		},
		components:{
			uniNavBar
		},
		props:['tabBars','currentTab'],
		methods:{
			// 切换导航栏
			changeTab(index){
				this.$emit('changeTabIndex',index)
			}
		}
	}
</script>

<style lang="scss">
	.uni-navbar{
		.left{
			.nav-left{
				text{
					font-size: 40upx;
					color: #FFA232;
				}
			}
		};
		.nav-center{
			width: 100%;
			display:flex;
			justify-content:center;
			.guanzhu{
				&:nth-of-type(1){
					flex: 1;
					text-align: right;
					padding: 0 10upx;
					position: relative;
					.nav-line{
						width: 60upx;
						height: 10upx;
						border-radius: 10upx;
						background-color: #FEDE33;
						position: absolute;
						top: 50upx;
						right: 7upx;
					}
				};
				&:nth-of-type(2){
					flex: 1;
					text-align: left;
					padding: 0 10upx;
					position: relative;
					.nav-line{
						width: 60upx;
						height: 10upx;
						border-radius: 10upx;
						background-color: #FEDE33;
						position: absolute;
						top: 50upx;
					}
				}
			}
		};
		.right{
			width:100%;
			.nav-right{
				text-align: right;
				text{
					font-size: 40upx;
					color:#333333
				}
			}
		}
	}
</style>
