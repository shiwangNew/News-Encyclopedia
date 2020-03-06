<template>
	<view class="chat-bottom">
		<input type="text" value="" placeholder="文明发言" v-model="text" />
		<view class="submit-button">
			<text class="icon iconfont icon-fabu" @tap='submitText()'></text>
		</view>
	</view>
</template>

<script>
	export default {
		data() {
			return {
				text:''
			};
		},
		methods:{
			// 发送输入内容、
			submitText(){
				this.$emit('submit',this.text)
				this.text = ''
			}
		}
	}
</script>

<style lang="scss" scoped>
	.chat-bottom{
		height: 120upx;
		position: fixed;
		bottom: 0;
		right: 0;
		left: 0;
		display: flex;
		justify-content: center;
		align-items: center;
		padding-left: 20upx;
		border-top: 1upx solid #EEEEEE;
		background-color: #fff;
		input{
			flex: 1;
			margin-right: 20upx;
			padding: 10upx 20upx;
			border-radius: 10upx;
			background: #F7F7F7;
		};
		.submit-button{
			width: 100upx;
			display: flex;
			justify-content: center;
			align-items: center;
			text{
				width: 60upx;
				font-size: 45upx;
				color: #000;
			};
		}
	}
</style>
