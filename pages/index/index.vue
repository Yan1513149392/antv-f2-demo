<template>
	<view class="content">
		<image class="logo" src="/static/logo.png"></image>
		<view class="text-area">
			<text class="title">{{title}}</text>
		</view>
		<canvas id="chartId"/>
	</view>
</template>

<script>
	const F2 = require('@antv/f2')
	export default {
		data() {
			return {
				title: 'Hello'
			}
		},
		onLoad() {
			
		},
		onReady() {
			this.chartInit()
		},
		methods: {
			chartInit(){
				const data = [{
				  day: '周一',
				  value: 300
				}, {
				  day: '周二',
				  value: 400
				}, {
				  day: '周三',
				  value: 350
				}, {
				  day: '周四',
				  value: 500
				}, {
				  day: '周五',
				  value: 490
				}, {
				  day: '周六',
				  value: 600
				}, {
				  day: '周日',
				  value: 900
				}];
				
				const chart = new F2.Chart({
				  id: 'chartId',
				  pixelRatio: window.devicePixelRatio
				});
				
				chart.source(data, {
				  value: {
				    tickCount: 5,
				    min: 0
				  },
				  day: {
				    range: [ 0, 1 ]
				  }
				});
				chart.tooltip({
				  showCrosshairs: true,
				  showItemMarker: false,
				  onShow: function onShow(ev) {
				    const items = ev.items;
				    items[0].name = null;
				    items[0].value = '$ ' + items[0].value;
				  }
				});
				chart.axis('day', {
				  label: function label(text, index, total) {
				    const textCfg = {};
				    if (index === 0) {
				      textCfg.textAlign = 'left';
				    } else if (index === total - 1) {
				      textCfg.textAlign = 'right';
				    }
				    return textCfg;
				  }
				});
				chart.line().position('day*value');
				chart.point().position('day*value').style({
				  stroke: '#fff',
				  lineWidth: 1
				});
				chart.render();
			}
		}
	}
</script>

<style>
	.content {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
	}

	.logo {
		height: 200rpx;
		width: 200rpx;
		margin-top: 200rpx;
		margin-left: auto;
		margin-right: auto;
		margin-bottom: 50rpx;
	}

	.text-area {
		display: flex;
		justify-content: center;
	}

	.title {
		font-size: 36rpx;
		color: #8f8f94;
	}
</style>
