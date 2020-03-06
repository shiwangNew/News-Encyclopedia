<template>
	<view class="nothing">
		<image src="../../static/common/nothing.png" 
				mode="widthFix"></image>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				
			};
		}
	}
</script>

<style lang="scss">
	.nothing{
		background: #FFFFFF;
		position: absolute;
		top: 0;
		left: 0;
		right: 0;
		bottom: 0;
		display: flex;
		justify-content: center;
		align-items: center;
		image{
			width: 50%;
		}
	}
</style>
