# 引入 ECharts
ECharts 3 开始不再强制使用 AMD 的方式按需引入，代码里也不再内置 AMD 加载器。因此引入方式简单了很多，只需要像普通的 JavaScript 库一样用 script 标签引入。
```
<!DOCTYPE html>
<html>
<header>
    <meta charset="utf-8">
    <!-- 引入 ECharts 文件 -->
    <script src="echarts.min.js"></script>
</header>
</html>
```

# demo01 柱状图的简单实现
基于准备好的dom，初始化echarts实例
`var myChart = echarts.init(document.getElementById('dom'));`
使用刚指定的配置项和数据显示图表。
`myChart.setOption(option);`
```
<!DOCTYPE html>
<html lang="en">
<head>
	<meta charset="UTF-8">
	<meta name="viewport" content="width=device-width, initial-scale=1,user-scalable=no"/>
	<title>Document</title>
	<script src="../dist/echarts.min.js"></script>
</head>
<body>
<!-- 为 ECharts 准备一个具备大小（宽高）的 DOM -->
<div id="main" style="width: 600px;height:400px;"></div>
<script type="text/javascript">
	// 基于准备好的dom，初始化echarts实例
	var myChart = echarts.init(document.getElementById('main'));
	// 指定图表的配置项和数据
	var option = {
		title: {
			text: 'ECharts 入门示例'
		},
		tooltip: {},
		legend: {
			data: ['销量']
		},
		xAxis: {
			data: ["衬衫", "羊毛衫", "雪纺衫", "裤子", "高跟鞋", "袜子"]
		},
		yAxis: {},
		series: [{
			name: '销量',
			type: 'bar',
			data: [5, 20, 36, 10, 10, 20]
		}]
	};
	// 使用刚指定的配置项和数据显示图表。
	myChart.setOption(option);
</script>
</body>
</html>
```
# demo02 折线图width toolbox 保存图片
 - 设置标题 `title.text`
 - 提示器 `tooltop.trigger`
 - 工具盒 `toolbox` 可以修改工具盒样式等，保存图片的样式等
 - 绘制区域间距 containLabel: false // 坐标轴刻度是否包含在间距内,true：不包含,false：包含
 - x轴
 - 系列列表
 
```javascript
option = {
	title: {
		text: '堆叠区域图'
	},
	tooltip: {
		trigger: 'axis'
	},
	legend: {
		data: ['邮件营销', '联盟广告', '视频广告', '直接访问', '搜索引擎']
	},
	toolbox: {
		feature: {
			saveAsImage: {
				show: true,
				name: "saveimg", // 点击保存图片默认名字
				type: "png", // 保存图片类型
				backgroundColor: "#f30",// 保存图片后的背景图（之前是png透明色或者jpg的白色）
				excludeComponents: true, // 保存为图片时忽略的组件列表，默认忽略工具栏。
				title: "click to save the img" // 图标文字提示
			}
		}
	},
	grid: {
		top: 50,
		left: 50,
		bottom: 50,
		right: 50,
		containLabel: false
	},
	xAxis: [
		{
			type: 'category',
			boundaryGap: false,
			data: ['周一', '周二', '周三', '周四', '周五', '周六', '周日']
		}
	],
	yAxis: {},
	series: [
		{
			name: '邮件营销',
			type: 'line',
			stack: '总量', // 加上堆叠式显示
			areaStyle: {normal: {}}, // 面积型展示
			data: [120, 132, 101, 134, 90, 230, 210]
		},
		{
			name: '联盟广告',
			type: 'line',
			stack: '总量',
			areaStyle: {normal: {}},
			data: [220, 182, 191, 234, 290, 330, 310]
		},
		{
			name: '视频广告',
			type: 'line',
			stack: '总量',
			areaStyle: {normal: {}},
			data: [150, 232, 201, 154, 190, 330, 410]
		},
		{
			name: '直接访问',
			type: 'line',
			stack: '总量',
			areaStyle: {normal: {}},
			data: [320, 332, 301, 334, 390, 330, 320]
		},
		{
			name: '搜索引擎',
			type: 'line',
			stack: '总量',
			label: {
				normal: {
					show: true,
					position: 'top'
				}
			},
			areaStyle: {normal: {}},
			data: [820, 932, 901, 934, 1290, 1330, 1320]
		}
	]
};
```
