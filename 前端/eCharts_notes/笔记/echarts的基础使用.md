# 使用五部曲

1. 导入echarts库文件
2. 设置一个容器
3. 初始化
4. 设置相关配置项（数据）
5. 将相关配置给到echarts实例对象





## 主要配置项

1. title

   标题组件，包含主标题和副标题。

2. tooltip
   提示框组件。

   > 鼠标经过时进行提示

3. legend
   图例组件。

4. toolbox
   工具栏。内置有导出图片、数据视图、动态类型切换、数据区域缩放、重置五个工具。

5. grid

   直角坐标系内绘图网格，单个 grid 内最多可以放置上下两个 X 轴，左右两个 Y 轴。

   ```javascript
   grid: {
   	left: '0%',
   	right: '0%',
   	bottom: '3%',
   	// 设置网格边距
   	containLabel: true
   	// 决定是否处理刻度溢出
   }
   ```

6. xAxis
   直角坐标系 grid 中的 x 轴。

   ```javascript
   xAxis: {
       type: 'category',
       // 坐标轴类型。['value', 'category', 'time', 'log']
       boundaryGap: false,
       // 坐标轴两边留白策略，类目轴和非类目轴的设置和表现不一样。
       data: ['Mon', 'Tue', 'Wed', 'Thu', 'Fri', 'Sat', 'Sun']
       // 类目数据，在类目轴（type: 'category'）中有效。
     },
   ```

7. color
   调色盘颜色列表。

8. series
   系列列表

   ```javascript
   series: [
       {
         name: 'Email',
         // 系列名称，用于tooltip的显示，legend 的图例筛选，在 setOption 更新数据和配置项时用于指定对应的系列。
         type: 'line',
         // 折线/面积图
         stack: 'Total',
         // 数据堆叠，同个类目轴上系列配置相同的stack值后，后一个系列的值会在前一个系列的值上相加。
         data: [120, 132, 101, 134, 90, 230, 210]
         // 该系列
       },
       {
         name: 'Union Ads',
         type: 'line',
         stack: 'Total',
         data: [220, 182, 191, 234, 290, 330, 310]
       },
       {
         name: 'Video Ads',
         type: 'line',
         stack: 'Total',
         data: [150, 232, 201, 154, 190, 330, 410]
       },
       {
         name: 'Direct',
         type: 'line',
         stack: 'Total',
         data: [320, 332, 301, 334, 390, 330, 320]
       },
       {
         name: 'Search Engine',
         type: 'line',
         stack: 'Total',
         data: [820, 932, 901, 934, 1290, 1330, 1320]
       }
     ]
   ```

   