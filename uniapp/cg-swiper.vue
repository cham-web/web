<template>
	<view class="" style="position: relative;">
		<swiper
			class="swiper"
			:indicator-dots="swiperDots"
			:autoplay="autoplay"
			:indicator-color="swiperColor"
			:circular="circular"
			:interval="interval"
			:duration="duration"
			:indicator-active-color="swiperActiveColor"
			@change="swiperChange"
		>
			<block v-for="(length, i) in count" :key="length">
				<swiper-item style="width: 100%;height: 360upx;">
					<view class="swiper-item">
						<view class="swiper-item-view" v-for="(item, index) in swiperList" :key="item.id" v-if="index> number*i-1 && index<number*(i+1)" @click="clickItem(item)">
							<view class="swiper-img">
								<image class="img" :src="item.iconUrl"></image>
							</view>
							<view class="text">{{ item.name }}</view>
						</view>
					</view>
				</swiper-item>
			</block>
		</swiper>
		<view class="dots" v-if="customize == true && swiperDots == false">
			<block v-for="(item, index) in count" :key="index">
				<view
					class="dot"
					:class="[index == swiperCurrent ? 'active' : '']"
					:style="[index == swiperCurrent ? { background: swiperActiveColor } : { background: swiperColor }]"
				></view>
			</block>
		</view>
	</view>
</template>

<script>
export default {
	name: 'cg-swiper',
	props: {
		// 面板指示点
		swiperDots: {
			type: Boolean,
			default: false
		},
		// 指示点颜色
		swiperColor: {
			type: String,
			default: '#999999'
		},
		// 选中指示点颜色
		swiperActiveColor: {
			type: String,
			default: '#FFCC00'
		},
		// 是否自动切换
		autoplay: {
			type: Boolean,
			default: false
		},
		// 自动切换时长
		interval: {
			type: Number,
			default: 5000
		},
		// 滑动动画时长
		duration:{
			type: Number,
			default: 500
		},
		// 是否采用衔接滑动
		circular: {
			type: Boolean,
			default: false
		},
		// 滑动块视图容器
		swiperList: {
			type: Array,
			default: function() {
				return [];
			}
		},
		// 是否开启自定义指示点
		customize: {
			type: Boolean,
			default: true
		},
		// 一屏显示的数量
		number: {
			type: Number,
			default: 8
		}
	},
	data() {
		return {
			swiperCurrent: 0
		};
	},
	computed:{
		count() {
			return new Array(Math.ceil(this.swiperList.length/this.number))
		}
	},
	methods: {
		swiperChange(e) { 
			this.swiperCurrent = e.detail.current
		},
		clickItem(item) {
			this.$emit('clickItem', item)
		}
	}
};
</script>

<style>
.swiper {
	width: 100%;
	height: 370upx;
	margin-top: 40rpx;
}
.swiper-item {
	display: flex;
	flex-wrap: wrap;
}
.swiper-item-view {
	/* display: flex;
	flex-direction: column;
	justify-content: center;
	align-items: center; */
	width: 17.5%;
	margin-right: 10%;
	text-align: center;
	height: 200upx;
}
.swiper-item-view:nth-of-type(4n) {
	margin-right: 0;
}
.swiper-img {
	width: 100%;
	height: 78rpx;
}
.img{
	width: 84rpx;
	height: 78rpx;
}
.text{
	color: #333333;
	font-size: 30rpx;
	margin-top: 10rpx;
}
/* 轮播圆点样式修改 */
.dots {
	/* position: absolute;
	left: 0;
	right: 0;
	bottom: 20upx; */
	display: flex;
	justify-content: center;
}
.dots .dot {
	margin: 0 5upx;
	width: 40upx;
	height: 6upx;
	border-radius: 6rpx;
	transition: all 0.6s;
}
.dots .dot.active {
	width: 40upx;
}
</style>
