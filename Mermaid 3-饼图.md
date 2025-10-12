# Mermaid 3:饼图

饼图（Pie chart），或称圆形图（circle chart）

使用关键字 `pie` 绘制饼图

- `pie` 之后可选的参数是 `showdata`，可以展示数据的数值

`title`：后直接接标题名称

数据集：饼图的扇区将按照标签的相同顺序顺时针排列

- 饼图中某个部分的标签，需放在双引号 "" 内
- 后跟冒号 : 作为分隔符
- 后跟正数值（支持最多两位小数）
- 详见示例代码：

```mermaid
%%{
    init{'theme':'forest'}
}%%

pie showData
    title Key elements in Product X
    "Calcium" : 42.96
    "Potassium" : 50.05
    "Magnesium" : 10.01
    "Iron" :  5
```
