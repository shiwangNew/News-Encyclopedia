<template>
	<view>
		<view class="load-more">
			{{loadtext}}
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
			loadtext: String
		}
	}
</script>

<style lang="scss" scoped>
	.load-more{
		text-align: center;
		padding: 0 0 7upx 0;
		color: #AAAAAA;
	}
</style>
