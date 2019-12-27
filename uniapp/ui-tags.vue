<template>
	<view class="tags">
		<scroll-view class="scroll-content" scroll-x="true">
			<view class="ul dis">
				<view class="li" v-for="(item, index) in values"  :class="current === index?'cur':''"  :key="index" @tap="onClickItem(index, item)">
					<view class="title">{{item.name}}</view>
					<view v-show="current === index" class="line"></view>
				</view>
			</view>
		</scroll-view>
	</view>
</template>

<script>
	export default {
		props:{
			values: { // 默认数组 [{name: '全部', name: '其他'}]
				type: Array,
				default: function() {
					return []
				}
			},
			current: { // 当前选中的值 默认 0
				type: Number,
				default: 0
			}
		},
		methods:{
			/**
			 * @param {Number} index = [value] 选中的当前的索引
			 * @param {Object} item = [value] 默认选中的对象
			 * */
			onClickItem(index, item) {
				// 向父组件传值
				// currentIndex 当前的索引， currentItem 当前选择的对象
				this.$emit('clickItem', {currentIndex: index, currentItem: item})
			}
		}
	}
</script>

<style lang="less" scoped>
	@import "~@/static/css/common.less";
	.tags {
		// width: 100%;
		// position: fixed;
		// top: calc(var(--status-bar-height) + 88rpx);
		// z-index: 99999;
		// background-color: white;
	}
	.scroll-content{
		.ul{
			.li{
				padding: 15rpx 15rpx;
				// margin-right: 30rpx;
				.title{
					white-space: nowrap;
					font-size: 30rpx;
					color: @black333;
				}
				&.cur{
					.title{
						color: @blue;
					}
				}
				.line{
					background-color: @blue;
					height: 9rpx;
					margin-top: 10rpx;
				}
			}
		}
	}
</style>
