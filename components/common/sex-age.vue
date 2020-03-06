<template>
	<view class="sex-age">
		<text class="icon iconfont" :class="[sex == 0?'icon-nan':'icon-nv']"><text>{{age}}</text></text>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		},
		props:{
			sex:Number,
			age:Number
		}
	}
</script>

<style lang="scss" scoped>
	.sex-age{
		display: inline-block;
		.icon-nv{
			background-color: #FF678D;
			padding: 6upx 10upx;
			border-radius: 40upx;
			font-size: 20upx;
		};
		.icon-nan{
			background-color: #44B3FF;
			padding: 6upx 10upx;
			border-radius: 40upx;
			font-size: 20upx;
		}
	}
</style>
