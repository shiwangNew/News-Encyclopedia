<template>
	<view>
		<view class="uni-list-cell cell-pd">
			<view class="uni-uploader">
				<view class="uni-uploader-head">
					<view class="uni-uploader-title">点击可预览选好的图片</view>
					<view class="uni-uploader-info">{{imageList.length}}/9</view>
				</view>
				<view class="uni-uploader-body">
					<view class="uni-uploader__files">
						<block v-for="(image,index) in imageList" :key="index">
							<view class="uni-uploader__file">
								<view class="delete_img" @tap="delete_img(index)">
									<text class="icon iconfont icon-biaoqing"></text>
								</view>
								<image class="uni-uploader__img" :src="image" :data-src="image" @tap="previewImage"></image>
							</view>
						</block>
						<view class="uni-uploader__input-box">
							<view class="uni-uploader__input" @tap="chooseImage"></view>
						</view>
					</view>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	var sourceType = [
		['camera'],
		['album'],
		['camera', 'album']
	]
	var sizeType = [
		['compressed'],
		['original'],
		['compressed', 'original']
	]
	export default {
		data() {
			return {
				imageList: [],
				sourceTypeIndex: 2,
				sourceType: ['拍照', '相册', '拍照或相册'],
				sizeTypeIndex: 2,
				sizeType: ['压缩', '原图', '压缩或原图'],
				countIndex: 8,
				count: [1, 2, 3, 4, 5, 6, 7, 8, 9],
			};
		},
		methods:{
			// 上传图片
			chooseImage: async function() {
				if (this.imageList.length === 9) {
					return;
				}
				uni.chooseImage({
					sourceType: sourceType[this.sourceTypeIndex],
					sizeType: sizeType[this.sizeTypeIndex],
					count: this.imageList.length + this.count[this.countIndex] > 9 ? 9 - this.imageList.length : this.count[this.countIndex],
					success: (res) => {
						this.imageList = this.imageList.concat(res.tempFilePaths);
						this.$emit('upload',this.imageList)
					},
					fail: (err) => {
						// #ifdef APP-PLUS
						if (err['code'] && err.code !== 0 && this.sourceTypeIndex === 2) {
							this.checkPermission(err.code);
						}
						// #endif
						// #ifdef MP
						uni.getSetting({
							success: (res) => {
								let authStatus = false;
								switch (this.sourceTypeIndex) {
									case 0:
										authStatus = res.authSetting['scope.camera'];
										break;
									case 1:
										authStatus = res.authSetting['scope.album'];
										break;
									case 2:
										authStatus = res.authSetting['scope.album'] && res.authSetting['scope.camera'];
										break;
									default:
										break;
								}
								if (!authStatus) {
									uni.showModal({
										title: '授权失败',
										content: 'Hello uni-app需要从您的相机或相册获取图片，请在设置界面打开相关权限',
										success: (res) => {
											if (res.confirm) {
												uni.openSetting()
											}
										}
									})
								}
							}
						})
						// #endif
					}
				})
			},isFullImg: function() {
				return new Promise((res) => {
					uni.showModal({
						content: "已经有9张图片了,是否清空现有图片？",
						success: (e) => {
							if (e.confirm) {
								this.imageList = [];
								res(true);
							} else {
								res(false)
							}
						},
						fail: () => {
							res(false)
						}
					})
				})
			},
			previewImage: function(e) {
				var current = e.target.dataset.src
				uni.previewImage({
					current: current,
					urls: this.imageList
				})
			},
			// 删除要上传的图片
			delete_img(index){ 
				uni.showModal({
				    title: '提示',
				    content: '确认删除？',
				    success: (res) => {
				        if (res.confirm) {
				            this.imageList.splice(index,1);
							this.$emit('upload',this.imageList)
				        }
				    }
				});
			}
		}
	}
</script>

<style lang="scss">
    .cell-pd {
		padding: 22upx 30upx;
		border-bottom: 1upx solid #EEEEEE;
		.uni-uploader__file{
			position: relative;
			.delete_img{
				position: absolute;
				top: 0;
				right: 0;
				background-color: #4c4c4c;
				padding: 5upx 10upx;
				border-radius: 8upx;
				z-index: 100;
				// line-height: 0;
				.icon{
					font-size: 48upx;
					color: #FFFFFF;
				}
			}
		}
	}
	uni-view{
		line-height: 1.2;
	}
	.list-pd {
		margin-top: 50upx;
	}
	.uni-list-cell::after{
		height: 0upx;
	}
</style>
