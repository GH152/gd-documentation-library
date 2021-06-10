# gd-documentation-library
UI库+逻辑库相关组件及方法说明文档

用法：
```javascript
npm i llgtfoo-components-boxs --save
```
在main.js中引入
```javascript
import llgtfooComponentsBoxs from 'llgtfoo-components-boxs'
import 'llgtfoo-components-boxs/dist/llgtfoo-components-boxs.css'
Vue.use(llgtfooComponentsBoxs)
注：全局使用,组件可以单独引用
```

   

| 组件：            |                          |
| :---------------- | ------------------------ |
| \<date-time/>     | 时间显示                 |
| \<select-date />  | 时间选中框               |
| \<number-scroll/> | 数字滚动                 |
| \<tab-page/>      | tab页切换、滚动(单个和一页滚动) |
| \<list-scroll/>   | 列表无缝滚动或者逐条滚动(支持事件暂停) |
| new this.$CMap()   | 集成cmap |
| **指令：**        |                          |
| v-auto-scale      | 大屏尺寸缩放             |
| v-water-marker    | 系统水印                 |
| v-drag | 鼠标自由拖拽 |
| **过滤器：**      |                          |
| \|numberFormat    | 格式化数字，如33,333     |



- 组件
  
    组件-1：
    
    ```
     <date-time>
    
        <template slot-scope="time">
    
         {{time.data.year}}-{{time.data.time}}
    
       </template>
    
    </date-time>    
    ```
    
    
    
    利用作用域插槽返回时间对象，自定义时间格式以及样式

```javascript
  data:{
         year, //年
          month,//月
          day,//日
          week,//星期几
          time//时间
  }
```

![](https://img-blog.csdnimg.cn/20200825204920689.png#pic_center)

 注：组件可以用容器包裹,来显示在不同的位置。

  组件-2：
 <select-date 
      :initYear="1996" 
      :styleObj='styleObj1'
      @getDate='getDate'></select-date>

```javascript
  initYear是初始年份,年下拉框显示当前年到初始年的所有年份
  styleObj1:{
    bg:'rgba(11, 41, 82, 0.5)',//选中框背景
    dropBg:'rgba(11, 41, 82, 0.8)',//下拉框背景
    hoverBg:'cyan',//下拉框选择鼠标滑过背景
    scale:0.5,//大小
    fontColor:'red'//字体颜色
  }
```
![](https://img-blog.csdnimg.cn/20200825204937277.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjg2OTA5,size_16,color_FFFFFF,t_70#pic_center)

 注：可选填其中几种；组件可以用容器包裹,来显示在不同的位置。

  组件-3：
  ```javascript
   <number-scroll class='llo' 
        :maxValue="maxValue" 
        :duration="duration"
        :separator="separator"
        :toFixed='toFixed'
        :prefix='prefix'
        :suffix='suffix'></number-scroll>

        maxValue:20000,//滚动数字的最大值，默认最大值2020
        duration:1000,//耗时，单位ms
        separator:',',//三位间隔符,默认没有字符
        toFixed:1 ,//保留小数,默认不保留
        prefix:'￥',//前缀，默认没有字符
        suffix:'单位'//后缀，默认没有字符

      注：可选填
  ```
注：数字样式自定义，例如类型llo

![](https://img-blog.csdnimg.cn/20200825204957655.png#pic_center)



 组件-4:

```javascript
 <tab-page :data='dataLists' :option='option1'>
        <ul class="list-box">
          <li v-for="(item,index) in dataLists" :key="index">{{item.name}}</li>
        </ul>
  </tab-page>
  dataLists:为数据
  ul为slot元素
  option1:{
        number:5,//默认显示五个
        single:true,//默认值false是一次性走动一页，true是一次性走动一个
        autoScroll:true,//自动滚动，默认false不滚动
        autoScrollTime:2000,//自动滚动时间间隔，默认3s，
        button:true,//左右两侧按钮显示
        （autoScroll为false，button必为true)
      },
   注：
       1.li如果有间隔，请向右间隔，即margin-right
       2.option1参数选填，可全不填
       3.移到元素上停止滚动效果，离开继续
```

![](https://img-blog.csdnimg.cn/20200825205015635.png#pic_center)

   

组件-5：

```javascript
         <div class="list-scroll-header" slot="header">
            <ul>
              <li
                v-for="(item,index) in headerList"
                :key="index"
                :style="{flex:`${item.width&&item.width}`}"
              >{{item.name}}</li>
            </ul>
          </div>//列表顶部标题
      <list-scroll v-if="dataScrollList.length>0" :option='scrollOption'      ref='scrollList'>
          <ul class="scroll-list" slot="main">
            <li v-for="(item,index) in dataScrollList" :key="index" id="child" ref="child">
              <span>{{item.name}}</span>
              <span>{{item.age}}</span>
              <span>{{item.marriage}}</span>
            </li>
          </ul>//列表滚动内容
        </list-scroll>
   参数：
   slot="header"为标题内容
   slot="main"为滚动内容
   dataScrollList为滚动数据,数据不为空的时候加载组件，计算组件高度
------------------------------------------------------------------------------
    scrollOption:{
        number:6,//默认显示几个
        seamless:true,//无缝滚动，默认true
        duration:2000//滚动时间间隔，无缝滚动时间间隔为此时间除以10
      },
          存在鼠标滚动
-------------------------------------------------------------------------------
      或者
       scrollOption:{
        number:6,//默认显示几个
        seamless:false,//单个过渡滚动，默认true
        duration:2000//滚动时间间隔，无缝滚动时间间隔为此时间除以10
      },
          鼠标操作无效，可以事件触发
     方法：
   可以利用ref调取函数
   sKeep()//继续滚动
   sStop()//停止滚动
-------------------------------------------------------------------------------------      
    注：选填几种，或者不填
    
  
```
![](https://img-blog.csdnimg.cn/20200830143140119.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjg2OTA5,size_16,color_FFFFFF,t_70#pic_center)

组件-6：
   CMap地图：
   ```
   集成cmap地图，只需new this.$CMap（options）即可使用
   用法： https://www.npmjs.com/package/@ektx/cmap
   ```

   ![](https://img-blog.csdnimg.cn/20200914195926289.png?x-oss-process=image/watermark,type_ZmFuZ3poZW5naGVpdGk,shadow_10,text_aHR0cHM6Ly9ibG9nLmNzZG4ubmV0L3FxXzMzMjg2OTA5,size_16,color_FFFFFF,t_70#pic_center)

- 指令：
  
     指令-1：

```javascript
v-auto-scale='{width: 1920, height: 1080}'
```

​    v-auto-scale用于根据自定义的尺寸缩放屏幕，一般用于大屏自适应

​     指令-2：

```javascript
v-water-marker='{
        width = '200px', //宽度
        height = '200px', //高度
        textAlign = 'center', //规定高度和宽度剧中
        textBaseline = 'middle', //垂直剧中
        font = '16px microsoft yahei', //字体
        fillStyle = 'rgba(184, 184, 184, 0.4)',  //颜色
        content = 'llgtfoo@163.com', //水印内容
        rotate = '-30', //水印水平倾斜角度
        zIndex = 1,  //水平层级，一般要低于页面的层级
        visible = true,//水印是否显示
}'
```

v-water-marker用于生成系统水印

![](https://img-blog.csdnimg.cn/20200825205031141.png#pic_center)

指令3：
```javascript
 v-drag="#top" 用于自由拖拽 
  
  #top是按指定区域可以拖拽，

  没值按整个区域都可以拖拽
```
- 过滤器 

     
  
   过滤器-1:
  
  ```javascript
  numberFormat 用于几位格式化数字
  numberFormat(
    {
      separator:'*',//符号
      step:4 //几位出现符号
  }
    )
  ```
  ![](https://img-blog.csdnimg.cn/20200825205045357.png#pic_center)
  
  
