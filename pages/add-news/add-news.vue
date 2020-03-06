<template>
	<view>
		<!-- 自定义导航栏 -->
		<uni-nav-bar :statusBar="true" rightText="发布" left-icon="back" @click-left="back" @click-right="saveNews" >
		<view class="allUser" @tap='onlyMine'>
			<text>{{privacy}}</text>
			<text class="icon iconfont icon-RectangleCopy"></text>
		</view>
		</uni-nav-bar>		
		<!-- text输入框 -->
		<view class="uni-text">
			<textarea  placeholder="说点什么吧~" v-model="text"/>
		</view>
		<!-- 上传多图 -->
		<upload-image @upload='upload'></upload-image>
		<!-- 告警框 -->
		<uni-popup ref="showpopup" :type="type" id="list">
			<view class="remindInfo">
				<image src="../../static/common/addinput.png" mode="widthFix" lazy-load></image>
				<view class="content">1、涉及黄色，政治，广告及骚扰信息</view>
				<view class="content">2、涉及人身攻击</view>
				<view class="content">3、留联系方式，透露他人隐私一经核实将被封禁，情节严重者永久封禁</view>
				<button type="primary" class="info-button" @tap="cancel('tip')">我已知晓</button>
			</view>
		</uni-popup>
	</view>
</template>

<script>
	let choose = ['所有人可见', '仅自己可见']
	import uniNavBar from '@/components/uni-nav-bar/uni-nav-bar.vue'
	import uploadImage from '../../components/upload-image/upload-image.vue'
	import uniPopup from '../../components/uni-popup/uni-popup.vue'
	export default {
		data() {
			return {
				privacy:'所有人可见',
				text:'',
				imageList:[],
				// 告警框是否展示
				showModel:true,
				type:''
			};
		},
		components:{
			uniNavBar,
			uploadImage,
			uniPopup
		},
		onShow() {
			// console.log('1')
			this.togglePopup('center', 'popup')
		},
		
		methods:{
			// 保存
			saveNews(){
				console.log('保存')
			},
			// 返回上一级
			// back(){
			// 	// console.log('返回')
			// 	uni.navigateBack({
			// 		delta:1
			// 	})
			// },
			back(){
				if((this.text !== '') || (this.imageList.length > 0)){
					uni.showModal({
						content: '是否要保存为草稿？',
						cancelText: '不保存',
						confirmText: '保存',
						success: res => {
							if(res.confirm){
								console.log("保存")
							}else{
								console.log("不保存")
							}
							// this.isget=true;
							uni.navigateBack({
								delta: 1
							});
						},
					});
				}
				uni.navigateBack({
					delta: 1
				});
			},
			// 更改可见范围
			onlyMine(){
				uni.showActionSheet({
					itemList: choose,
				    success:  (res) => {
				        // console.log('选中了第' + (res.tapIndex + 1) + '个按钮');
						// console.log(choose[res.tapIndex])
						this.privacy = choose[res.tapIndex]
				    },
				    fail: function (res) {
				        console.log(res.errMsg);
				    }
				});
			},
			// 上传图片
			upload(imageArr){
				this.imageList = imageArr
				// console.log(this.imageList)
			},
			// 告警框
			onBackPress() {
				this.$refs['showpopup'].close()
			},
			togglePopup(type, open) {
				this.type = type
				this.$nextTick(() => {
					this.$refs['show' + open].open()
				})
			},
			cancel(type) {
				// this.$refs['show' + type].close()
				// this.$refs.uniPopup.close(type)
				this.selectComponent("#list").close();
			}
		}
	}
</script>

<style lang="scss" scoped>
	.allUser{
		width: 100%;
		display: flex;
		justify-content: center;
		align-items: center;
	}
	.uni-text{
		width: 100%;
		border:1upx solid #EEEEEE;
		padding: 10upx;
	}
	.remindInfo{
		background-color: #FFFFFF;
		padding: 15upx;
		width: 600upx;
		text-align: center;
		image{
			width: 60%;	
			margin-bottom: 20upx;
		}
		.content{
			text-align: left;
			color: #0A0A0A;
			line-height: 45upx;
		}
		.info-button{
			background-color: #FFE934;
			margin-top: 20upx;
			color: #0A0A0A;
		}
	}
</style>
