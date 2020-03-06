<template>
	<view class="cross-corr animated fadeIn fast">
		<view class="corr-ava">
			<image :src="item1.userpic" mode="widthFix" lazy-load></image>
		</view>
		<view class="corr-info">
			<view class="corr-name">
				<text>{{item1.username}}</text>
			</view>
			<sex-age :age="item1.age" :sex="item1.sex"></sex-age>
		</view>
		<view class="corr-foll">
			<text class="icon iconfont" :class="[item1.isguanzhu?'icon-xuanze1':'icon-zengjia1']"></text>
		</view>
	</view>
</template>

<script>
	import sexAge from '../common/sex-age.vue'
	export default {
		data() {
			return {
				
			};
		},
		components:{
			sexAge
		},
		props:{
			item1: Object,
			index1: Number
		}
	}
</script>

<style lang="scss" scoped>
	.cross-corr{
		padding: 20upx;
		display: flex;
		border-bottom: 1px solid #EDEDED;
		align-items: center;
		justify-content: center;
		&:last-child{
			border-bottom: none;
		}
		.corr-ava{
			width: 120upx;
			display: flex;
			align-items: center;
			image{
				width: 100upx;
				border-radius: 50%;
			}
		};
		.corr-info{
			flex: 1;
			padding-right: 10upx;
			.corr-name{
				font-size: 35upx;
				font-weight: 600;
			};
		};
		.corr-foll{
			width: 100upx;
			text-align: right;
			.icon{
				color: #ccc;
			}
			.icon-zengjia1{
				color: #F98734;
			}
		}
	}
</style>
