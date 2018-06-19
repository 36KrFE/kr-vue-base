# 鲸准·洞见 Less开发规范

- 2018-04-28 创建

### 开发规约

- 2个空格缩进
- 非特殊情况禁止使用 `标签选择器` ，如果使用了，请加注释说明原因
- 非特殊情况禁止使用 `!important` ，如果使用了，请加注释说明原因
- 非特殊情况禁止使用 `内联样式`，如果使用了，请加注释说明原因
- 非特殊情况禁止使用 `calc` ，如果使用了，请加注释说明原因
- 每一个 `:` 后面必须保留一个空格
- 每一个 `,` 后面必须保留一个空格
- 每一个 `{` 前面必须保留一个空格
- 对于任何小于1的属性值，不允许省略前面的0，比如透明度 .1 // bad -> 0.1 // good
- 为了代码的易读性和可维护性，禁止使用简写
- 类名命名规则
 - 类名只允许包含小写字母，-，_
 - [页面名字空间]\__[节点名字空间]-[元素]。例如：home\__header-logo, home\__section, home\__main-avatar
 - [页面名字空间]可以省略，前提是必须保证在该页面名字空间下
 - 类名必须有意义，能够清晰表达是关联的哪个Dom元素
- 减少使用选择器，会影响性能
- less文件名使用小写字母，-，例如：app-header.less
- less变量以小驼峰法命名
- less函数名规则同类名

*Note*: 一旦使用颜色相关的样式，需要通过less函数的方式从 `theme` 函数引入。由于函数会替换为其内部的代码。所以需要在一个具体的less类中使用函数，而不是直接使用。

### 目录结构

```hash
|-- /styles/
|   |-- /[主题名]/ // 主题目录
|   |   |-- /index.less // 皮肤色值定义文件
|   |-- /common/ // 样式主体
|   |   |-- /index.less // 暴露对外接口，
|   |   |-- /base.less // 通用变量以及样式，如字号，字体，字重，边框，函数
|   |   |-- /components/ // 基础组件样式
|   |   |-- /views/ // 页面样式
|   |   |   |-- /[页面名称].less // 页面相关的逻辑组件单元
|   |   |-- /fragments /// 功能组件
|   |   |   |-- /[功能组件名].less // 比如表单，图表
|   |-- /index.less // 对外暴露接口
```

### /styles/index.less 对外接口文件

```less
  // 引入主题定义文件
  @import './[主题名]/index.less';
```

### /styles/[主题名]/index.less 主题定义文件

```less
  // 引入样式主体
  @import './../common/index.less';

  .[主题名字空间] {
    // 执行皮肤函数
    .theme(
      // 各种皮肤颜色参数
      @titleColor: #fff;
      @normalBGColor: #eee;
      ...
    )
  }
```

### /styles/common/base.less 通用样式文件

```less
  // 涉及到颜色与换肤相关的使用less函数
  .font-main-title(@fontColor) {
    font-size: 24px;
    color: @fontColor;
    font-weight: 500;
  }

  // 不涉及换肤相关的使用less类
  .font-main-subtitle {
    font-size: 18px;
    font-weight: 400;
  }
  ...
```

### /styles/common/index.less 对外暴露接口
需要将自己添加的页面样式，组件样式，引入到这里然后添加到主函数内部，并传入自己页面或组件需要的颜色变量。

```less
  // *****该文件每次增加变量必须添加注释*****
  .theme(
    @[变量名], // 注释
  ) {
    .[页面名字空间名](@[需要的颜色变量]); // 页面
    .[组件名字空间名](@[需要的颜色变量]); // 如果是通用组件需要在这里，如果是页面内自己的内部组件，在页面内部处理
  }
```

### /styles/common/components/[组件名].less 组件样式

```less
  // 涉及到颜色与换肤相关的使用less函数
  .menu__menu-wrapper(@fontColor) {
    font-size: 24px;
    color: @fontColor;
    font-weight: 500;
  }

  // 不涉及换肤相关的使用less类
  .menu__menu-wrapper {
    font-size: 18px;
    font-weight: 400;
  }
  ...
```

### /styles/common/views/[页面名].less 页面样式

```less
  // 涉及到颜色与换肤相关的使用less函数
  .user__container(@fontColor) {
    font-size: 24px;
    color: @fontColor;
    font-weight: 500;
  }

  // 不涉及换肤相关的使用less类
  .user__container {
    font-size: 18px;
    font-weight: 400;
  }
  ...
```


### /styles/common/fragments/[功能组件名].less 功能组件样式

```less
  // 涉及到颜色与换肤相关的使用less函数
  .navigator(@fontColor) {
    font-size: 24px;
    color: @fontColor;
    font-weight: 500;
  }

  // 不涉及换肤相关的使用less类
  .navigator {
    font-size: 18px;
    font-weight: 400;
  }
  ...
```