<template>
	<view>
		<view class="status_bar"></view>
		<view class="navbar">
			<view class="navbar-back" v-if="backFlag"  @tap="handleBack">
				<uni-icons class="back" type="arrowleft" size="30" color="#fff"></uni-icons>
				<!-- <image class="back" src="../../static/img/icon-back.png" mode="aspectFit"></image> -->
			</view>
			<view v-if="inputFlag" class="form-group">
				<view class="form-input">
					<input class="input" type="text" :disabled="disabled" :placeholder="i18n.search" v-model="searchForm" @tap="handleSearch" placeholder-style="color: #999" confirm-type="search" @confirm="handleSelectLanuage" />
				</view>
			</view>
			<view v-else class="text">{{title}}</view>
			<view v-if="languageFlag" class="imgs" @tap="handleSelectLanuage">
				<image class="img" :src="icon" mode="aspectFit"></image>
			</view>
			<view v-if="confirmFlag" class="confirm" @tap="handleEdit">{{edit}}</view>
		</view>
	</view> 
</template>

<script>
	import { uniIcons } from '@dcloudio/uni-ui'
	export default {
		components:{
			uniIcons
		},
		props: {
			inputFlag: { // 是否显示input输入框
				type: Boolean,
				default: false
			},
			disabled: { // 是否禁用输入框
				type: Boolean,
				default: false
			},
			backFlag: { // 是否显示返回图标
				type: Boolean,
				default: false
			},
			title: { // navbar标题
				type: String,
				default: '商城'
			},
			icon: { // languageFlag 为true icon显示的图标
				type: String,
				default: '../../static/img/icon-language-default.png'
			},
			languageFlag: {
				type: Boolean,
				default: false
			},
			edit: { // confirmFlag 为true 右侧显示文字
				type: String,
				default: '完成'
			},
			confirmFlag: {
				type: Boolean,
				default: false
			}
		},
		data() {
			return {
				searchForm: '' // 搜索双向绑定的值
			}
		},
		computed:{
			i18n() {
				return this.$t('common')
			}
		},
		methods: {
			/**
			 * 监听返回事件
			 * */
			handleBack() {
				this.$emit('handleBack')
			},
			// 监听右上角图片事件 languageFlag 为true时
			handleSelectLanuage() {
				if(this.inputFlag) {
					this.$emit('handleSelectLanuage', this.searchForm)
				} else {
					this.$emit('handleSelectLanuage')
				}
			},
			// 监听右上角文字事件 confirmFlag 为true时
			handleEdit(){
				this.$emit('handleEdit')
			},
			// 监听搜索按钮
			handleSearch() {
				this.$emit('handleSearch')
			}
		}
	}
</script>

<style lang="less" scoped>
.navbar {
	width: 100%;
	position: fixed;
	top: var(--status-bar-height);
	height: 88rpx;
	background: linear-gradient(0, #0ab4f1, #0ba3f1);
	text-align: center;
	z-index: 10;
	display: flex;
	align-items: center;
	.navbar-back{
		width: 88rpx;
		height: inherit;
		position: absolute;
		left: 0;
		top: 0;
		text-align: center;
		.back{
			width: 22rpx;
			height: 38rpx;
			vertical-align: -webkit-baseline-middle;
		}
	}
	.text {
		width: 75%;
		color: white;
		font-weight: bold;
		line-height: 88rpx;
		overflow: hidden;
		text-overflow:ellipsis;
		white-space: nowrap;
		margin-left: auto;
		margin-right: auto;
	}
	.imgs{
		position: absolute;
		display: block;
		width: 88rpx;
		height: 88rpx;
		margin-left: auto;
		top: 0;
		right: 0;
		display: flex;
		align-items: center;
		justify-content: center;
		.img{
			width: 50rpx;
			height: 43rpx;
		}
	}
	.confirm{
		position: absolute;
		width: auto;
		height: 88rpx;
		font-size: 30rpx;
		top: 0;
		right: 0;
		text-align: center;
		line-height: 88rpx;
		color: white;
		padding-right: 20rpx;
	}
}
.form-group{
	width: 78%;
	height: 60rpx;
	background-color: #f7f7f7;
	margin-left: auto;
	margin-right: auto;
	display: flex;
	align-items: center;
	border-radius: 60rpx;
	.form-input{
		width: 100%;
		padding-left: 26rpx;
		padding-right: 26rpx;
		.input{
			text-align: left;
			font-size: 26rpx;
		}
	}
}
</style>
