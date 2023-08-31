# 什么是BFC
    BFC(block formatting context)是页面上的一个小型布局形式，所有在BFC里面的元素不会影响到BFC外面的元素。值得一提的是，FLex或Grid容器可以创造出Flex或Grid格式上下文，类似BFC，我们也可以称其为FFC或GFC。FFC和GFC跟BFC很相似，除了一点，FFC和GFC里不能存在浮动子元素。但是FFC和GFC仍然可以解决外部浮动和margin折叠的问题。例如下面这个例子：
```html
<!DOCTYPE html>
<html lang="en">
  <head>
    <meta charset="UTF-8" />
    <meta name="viewport" content="width=device-width, initial-scale=1.0" />
    <meta http-equiv="X-UA-Compatible" content="ie=edge" />
    <title>Flex formatting context</title>

    <style>
        .red {
          background: lightpink;
          height: 50px;
          margin: 10px;
          float: left;
        }

        .blue {
           background: lightblue;
           height: 50px;
           margin: 10px;
        }
        .flexbox {
         display: flex;
        }
    </style>
  </head>
  <body>
    <div class="flexbox">
      <div class="blue"><p>I am a blue flex item</p></div>
      <div class="blue"><p>I am a blue flex item</p></div>
      <div class="blue"><p>I am a blue flex item</p></div>
      <div class="red"><p>I am a red flex item with float left</p></div>
    </div>
  </body>
</html>

```
# 如何创建BFC
   有很多种方法可以创建BFC：
1. 文档的根元素（\<html\>）。
2. 浮动元素（即 float 值不为 none 的元素）。
3. 绝对定位元素（position 值为 absolute 或 fixed 的元素）。
4. 行内块元素（display 值为 inline-block 的元素）。
5. 表格单元格（display 值为 table-cell，HTML 表格单元格默认值）。
6. 表格标题（display 值为 table-caption，HTML 表格标题默认值）。
7. 匿名表格单元格元素（display 值为 table（HTML 表格默认值）、table-row（表格行默认值）、table-row-group（表格体默认值）、table-header-group（表格头部默认值）、table-footer-group（表格尾部默认值）或 inline-table）。
8. overflow 值不为 visible 或 clip 的块级元素。
9. display 值为 flow-root 的元素。
10. contain 值为 layout、content 或 paint 的元素。
11. 弹性元素（display 值为 flex 或 inline-flex 元素的直接子元素），如果它们本身既不是弹性、网格也不是表格容器。
12. 网格元素（display 值为 grid 或 inline-grid 元素的直接子元素），如果它们本身既不是弹性、网格也不是表格容器。
13. 多列容器（column-count 或 column-width (en-US) 值不为 auto，且含有 column-count: 1 的元素）。
14. column-span 值为 all 的元素始终会创建一个新的格式化上下文，即使该元素没有包裹在一个多列容器中（规范变更、Chrome bug）
格式化上下文影响布局，通常，我们会为定位和清除浮动创建新的 BFC，而不是更改布局，因为它将：
- 包含内部浮动。
- 排除外部浮动。
- 阻止外边距重叠。

一个新的 display 属性的值，它可以创建无副作用的 BFC。在父级块中使用 display: flow-root 可以创建新的 BFC。