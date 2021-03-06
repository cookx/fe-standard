# 项目目录结构规范

## 规范说明

本规范适用于`业务项目`和`包`项目。

app表示一个项目，$root表示项目的根目录。

将文件资源分为两大类：`代码资源`和`内容资源`。

## 目录命名原则

1. 语义化

使用行业内常用命名，尽量不使用不易理解的缩写。参考[常用目录结构参考](xiang-mu-mu-lu-jie-gou-gui-fan.md#常用目录结构参考)

1. 简洁
2. 有复数的，使用复数形式。

例：`assets`, `images`等。

## 目录层级划分原则

### 根目录划分

项目根目录按照职能进行划分。

常用的目录有`src`、`dist`、`build`、`docs`、`mock`等。详细请参考[一级目录详细说明](xiang-mu-mu-lu-jie-gou-gui-fan.md#一级目录说明)

### 根据业务逻辑划分src目录结构

业务逻辑放在`src`目录中，先根据功能模块划分目录结构，子目录根据业务模块划分目录。参考[常用目录结构参考](xiang-mu-mu-lu-jie-gou-gui-fan.md#常用目录结构参考)

例： 按功能模块划分：`plugins`，`components`，`assets`，`pages`，`store`等。

按业务模块划分：`pages`目录下分`user`，`order`，`activities`

#### 业务目录划分原则

对于页面中的`HTML`、`JS`、`CSS`等代码资源，放在当前业务模块下。

当`JS`、`CSS`较大时，可独立出来，放入`assets`目录中。

页面中的内容资源`图片`、`icon`、`字体`等，放入`assets`目录中。

业务目录中，如果文件太多不好管理，需要划分子目录时，应遵守根据业务目录划分原则，划分子业务。

```text
src
    pages
        bus/
            images/
                icon1.png
            bus.js
            bus.html
            bus.css
```

## 常用目录结构参考

### 一级目录说明

`src`：开发源文件

`dist`：编译后的产出目录

`build`：项目编译原代码

`docs`：项目文档。包括开发文档、资源文档、备注文档。

`mock`：假数据

`static`：不需编译的外部资源

`test`：测试脚本

`config`：项目编译配置

### src目录说明

可根据项目需要自由组合。

`common`：公用模块

`plugins`：js插件

`components`：公用组件

`assets`：资源文件

```text
`styles`：从页面抽离的CSS
`icons`：icon小图标 iconfont / SVG
`images`：图片
```

`pages`：页面

`store`：状态管理（数据驱动框架）

`dao`：数据层，与`store`二选一

`apis`：ajax request 抽离

`routes`：路由

`config`：配置中心

### 总的目录结构

```bash
app
|---build  # 编译配置
|
|---docs   # 项目文档
|
|---dist    # 产出目录
|
|---src    # 开发目录
|     |---common    # 公用模块
|     |---plugins    # JS插件
|     |---components    # 项目公用组件
|     |---assets    # 资源文件
|     |     |- images   # 图片
|     |     |- icons    # iconfont/svg
|     |     |- stylus   # stylus
|     |---pages    # 页面
|     |     |- user   # 用户业务模块
|     |     |   |- components    # 当前页面组件
|     |     |   |- index.vue    # 页面(index.html、index.css、index.js)
|     |---store/dao    # 状态管理/数据逻辑层
|     |---apis    # ajax 抽离
|     |---routes    # 路由
|     |---config    # 页面内部变量配置
|
|---static    # 不需编译的外部资源
|
|---mock   # 数据模拟
|
|---test    # 测试脚本
|
|---config    # 项目编译配置
```

