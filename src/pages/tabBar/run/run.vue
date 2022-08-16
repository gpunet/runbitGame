<template>
	<view class="content">
		<view class="bg">

			<view class="uni-flex uni-row" style="margin: 1.425rem; height: 89.44rpx; ">
				<img class="flex-item" src="../../../static/heard.png" style="width:3.125rem;" />
				<img class="currentImg" src="../../../static/Ellipse38.png" />
				<view class="currentbs">在线3000步</view>
				<img class="userName" src="../../../static/Group3.png" />
			</view>

<view style="margin-top: 123.88rpx; height:69.44rpx ; width: 90%; margin-left: 5%; ">
				<u-subsection activeColor="#FFEB34" font-size="15" :list="list"  mode="subsection"  :current="curNow" @change="sectionChange"></u-subsection>
				<view >
					<view v-if="curNow === 0">
						<view class="uni-flex uni-row"  style="display: flex; margin:1rem 0px; height: 85.55rpx; width: 100%; ">
							<view style="width: 50%; margin: auto 0; ">
								 <uni-data-select
								        v-model="value"
								        :localdata="range"
								        @change="change"
								      ></uni-data-select>
							</view>
							<view @click="actionSheetTap" class="fillter">Fillter(0)</view>
							<image @click="actionSheetTap"  class="filltericon" src="../../../static/Frame3.png"></image>
							
						</view>
						<oct-goods :lists="goodsArr" price-type="$" @onGoods="onGoods" />
					</view>
					<view v-if="curNow === 1"><text class="content-text">选项卡2的内容</text></view>
				</view>
</view>
		</view>

	</view>
</template>

<script>
	export default {
		data() {
			return {
				buttonRect: {},
				value:"请选择",
				goodsArr: [
				    {
				        goods_id    : "",
				        cover       : "https://t7.baidu.com/it/u=852388090,130270862&fm=193&f=GIF",
				        name        : "茅台王子酒 金王子 53度 500毫升",
				        price       : {
				            price_min: 275
				        }
				    },{
				        goods_id    : "",
				        cover       : "https://t7.baidu.com/it/u=1092574912,855301095&fm=193&f=GIF",
				        name        : "飞天53%vol 500ml贵州茅台酒（带杯）",
				        price       : {
				            price_min: 1499
				        }
				    }
				],
			 range: [
			          { value: 0, text: "美观性" },
			          { value: 1, text: "舒适性" },
			          { value: 2, text: "功能性" },
			        ],
				curNow: 0,
				 list: ['运动装备', '属性卡'],
				current: 0,
				colorIndex: 0,
				items: ['选项卡1', '选项卡2'],
				styleType: 'button',
				activeColor: '#FFEB34',
			}
		},
		methods: {
			actionSheetTap() {
				const that = this
				uni.showActionSheet({
					title: '装备筛选',
					itemList: ['鞋子', '裤子', '上衣'],
					popover: {
						// 104: navbar + topwindow 高度，暂时 fix createSelectorQuery 在 pc 上获取 top 不准确的 bug
						top: that.buttonRect.top + 104  + that.buttonRect.height,
						left: that.buttonRect.left + that.buttonRect.width / 2
					},
					success: (e) => {
						console.log(e.tapIndex);
						uni.showToast({
							title: "点击了第" + e.tapIndex + "个选项",
							icon: "none"
						})
					}
				})
			},
			onGoods(){},
			sectionChange(index) {
							this.curNow = index;
						},
			onClickItem(e) {
				if (this.current !== e.currentIndex) {
					this.current = e.currentIndex
				}
			},
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100%;

	}

	.bg {
		position: absolute;
		width: 100%;
		height: 8.875rem;
		left: 0px;
		top: 0px;
		background: linear-gradient(180deg, #FFF7B0 0%, rgba(255, 247, 176, 0) 100%);
		border-radius: 0px 0px 36px 36px;
	}

	.currentbs {
		display: flex;

		flex-direction: row;
		font-weight: bold;
		align-items: center;
		margin-left: 0.425rem;
	}

	.currentImg {
		width: 0.625rem;
		height: 0.625rem;
		display: block;
		margin: auto 0;
		margin-left: 0.825rem;
	}

	.userName {
		display: block;
		margin: auto 0;
		margin-left: 1.1rem;
		width: 9rem;
		height: 2.25rem;
	}
	.fillter{
		margin: auto 0;
		margin-left: 126.94rpx;
	}
	.filltericon{
		
		width: 50.83rpx;
		height:45.83rpx;
		margin: auto 0;
		padding-top: 18.94rpx;
		
	}
</style>
