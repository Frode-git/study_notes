## flex布局

- 基本使用方法：给需要设置为弹性布局元素的父盒子设置`displat:flex`

- flex模型说明

  > 当元素表现为flex框时，它们沿着两个轴来布局：

  ![image-20220323145752593](E:\study_notes\前端\Css_notes\布局\Untitled.assets\image-20220323145752593.png)

  - **主轴(main axis)** 是沿着flex元素放置的方向延伸的轴（比如页面上的横向的行、纵向的列）。该轴的开始和结束被称为 **main start** 和 **main end**。
  - **交叉轴（cross axis）** 是垂直于flex元素放置方向的轴。该轴的开始和结束被称为**cross start** 和 **cross end**。
  - 设置了`display：flex`的父元素被称为**flex容器**（flex container)。
  - 在flex容器中表现为柔性的盒子的元素被称之为**flex项（flex item）**

- 属性设置

  - flex-direction: row / column;

    > 1. 该属性可以指定主轴的方向（弹性盒子子类放置的地方）——它默认是 `row`，这使得它们在按你浏览器的默认语言方向排成一排（在英语/中文浏览器中是从左到右）。
    >
    > 2. 设置成 `column`主轴方向变成垂直方向
    > 3. 还可以使用`row-reverse`和`column-reverse`**反向**排列flex项目

  - 换行设置

    > 当我们在布局中使用定宽或者定高的时候，可能会出现 flex项 溢出，破坏布局的现象，可通过如下设置进行解决。

    - 设置容器盒子 `flex-wrap: wrap`
    - 设置flex项 `flex: 200px`

    > 1. 通过以上第一个设置，实现了自动换行，通过第二个设置，实现了每个 flex项 的宽度至少是 200px。但我们会注意到最后几项可能会出现变得很宽，以便填满整行的现象。
    > 2. 这里还可以将 `flex-direction`的属性值改为 `row-reverse`，我们会发现是将每一行逆序排列

  - 上述两种属性还可以使用缩写的方式

    > `flex-direction` 和 `flex-wrap`的缩写：`flex-flow`。
    >
    > 比如：
    > 	`flex-direction: row`
    > 	`flex-wrap: wrap`
    >
    > 可以缩写为：
    >
    > ​	`flex-flow: row wrap`

  - flex 项的动态尺寸

    - 设置 flex项 `flex: 1`

    > 1. 这是一个无单位的比例值，表示每个 flex项 沿主轴的可用空间大小。因为它是一个比例，所以将每个 flex项 的flex设置为4000和设置为1的效果是完全一样的。
    > 2. 将不同的 flex项 的flex设置不同的值，可以控制相应的宽度占比（`flex-direction: row`)。
    > 3. 在设置展宽比例的基础上，还可设置最小宽度`flex: 1 200px`。此时，每个 flex项 将首先给出200px的可用空间，然后将剩余的可用空间根据比例进行分配

  - flex: 缩写与全写

    > `flex`是一个可以指定最多三个不同值的缩写属性:
    >
    > 1. 第一个就是上面所述的无单位比例（可以单独指定全写`flex-grow`属性的值
    > 2. 第二个无单位比例`flex-shrink`，一般用于溢出容器的flex项。这指定了从flex项中取出多少溢出量，以阻止它们溢出它们的容器。
    > 3. 第三个是上面讨论的最小值（可以单独指定全写`flex-basis`属性的值。

  - 垂直和水平居中

    1. `align-items`控制 flex项 在交叉轴上的位置（给flex容器设置）。

       > 1. 默认的值是 `stretch`，会使所有 flex项 沿着交叉轴的方向拉伸以填充父容器。如果父容器在交叉轴方向上没有固定高度，则所有 flex项 将变得与最长的 flex项 一样高。
       > 2. 使用`center`会使这些项保持其原有的高度，但是会在交叉轴居中。
       > 3. 还可以使用`flex-start`和`flex-end`实现在交叉轴的开始处或结束处对齐。
       > 4. 还可通过给flex项设置`align-self`属性覆盖`align-items`的行为。

    2. `justify-content`控制 flex项 在主轴上的位置。

       > 1. 默认值是`flex-start`，这会使所有flex项都位于主轴的开始处。
       > 2. `flex-end`让 flex项 位于结尾处。
       > 3. `center`在 `justify-content`里也可使用，可让 flex项 在主轴居中。
       > 4. `space-round`使所有 flex项 沿着主轴均匀地分布，在任意一端都会留有一点空间。
       > 5. 还有一个值是`space-between`，它和`space-around`非常相似，只是它不会在两端留下任何空间。

  - flex项排序

    > 1. 弹性盒子也有可以改变 flex项 的布局位置的功能，但不会影响到dom树里的元素的顺序。
    > 2. 使用方法：给flex项 添加`order: 1 / 具体的值`
    > 3. 默认的 `order` 值为 0，`order`值越大越排在后面。
    > 4. 可以设置为负值，从而使之排在最前面。