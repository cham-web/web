<template>
	<view>
		<view class="cell" @tap="handleClick">
			<view class="dis" :class="padding?'':'app-container'">
				<view class="left">{{title}}</view>
				<view class="right">
					<uni-icons v-if="arrow" type="arrowright" size="20" color="#333"></uni-icons>
					<template v-else>
						<text v-if="right">{{right}}</text>
						<uni-icons v-if="obj" class="icon" type="trash" color="#DA2811" size="24" @click="handleDel"></uni-icons>
					</template>
				</view>
			</view>
		</view>
	</view>
</template>

<script>
	import { uniIcons } from '@dcloudio/uni-ui'
	export default {
		props:{
			padding: {
				type: Boolean,
				default: false
			},
			arrow: { // 是否显示箭头
				type: Boolean,
				default: true
			},
			right: { // 右侧默认显示的文字
				type: String,
				default: null
			},
			title: { // 左侧显示的标题内容
				type: String,
				required: true,
				default: '标题'
			},
			del: { 
				type: Boolean,
				default: false
			},
			obj: { // 删除需要传的对象
				type: Object,
				default: function() {
					return null
				}
			}
		},
		components:{
			uniIcons
		},
		methods:{
			handleClick() {
				// 父组件的点击事件
				this.$emit('handleClick')
			},
			handleDel() {
				// 向父组件传值 当前的obj obj有内容时
				this.$emit('handleDel', this.obj)
			}
		}
	}
</script>

<style lang="less" scoped>
	@import "~@/static/css/common.less";
	@blackf7: #f7f7f7;
	@black333: #333;
	@blue: #3D97FF;
	.cell{
		font-size: 28rpx;
		
		padding: 40rpx 0;
		border-bottom: solid 2rpx @blackf7;
		
		.dis{
			align-items: center;
			justify-content: space-between;
			.left{
				color: @black333;
			}
			.right{
				color: @blue;
			}
		}
		
	}
	.icon{
		margin-left: 30rpx;
	}
</style>
