# sass

## 安装

`npm install sass --save`
依赖`node-sass`和`sass-loader`

### 离线环境安装node-sass

1. 首先需要download node-sass Binary文件
    运行`node -p "[process.platform, process.arch, process.versions.modules].join('-')"`获取版本
2. 下载地址: [cnpm](https://npm.taobao.org/mirrors/node-sass) [GitHub](https://github.com/sass/node-sass/releases)
`win32-x64-57` 则下载 `win32-x64-57_binding.node`
3. 将下载好的Binary文件存放在本地后指定node-sass源文件地址
`npm config set sass-binary-path C:/xxx...xxx/win32-x64-57_binding.node`
4. 最后使用`npm install node-sass`进行安装

> [参考文章](http://ju.outofmemory.cn/entry/73170)

## 使用

### sass文件监视器的创建：

监听命令: 
`node-sass -w xxx.scss xxx.css --output-style expanded`

### SASS提供四个编译风格的选项：

* nested：嵌套缩进的css代码，它是默认值。
* expanded：没有缩进的、扩展的css代码。
* compact：简洁格式的css代码。
* compressed：压缩后的css代码。

## 语法

### 1.变量

变量以`$`开头，在字符串中用`#{}`包裹

```scss
$side: left;
.border {
    border-#{$side}: 1px solid #000;
}
```

变量也可以类似数组和对象，使用`list`和`map`表示：
`list: $px: 1px 2px 3px;` 取值：`nth($px, 1)`， 即 `1px`
`map: $px: (S: 8px, M: 16px, L: 24px)` 取值：`map-get($px, S)`，即 `8px`

### 2.嵌套

`&` 引用父元素

### 3.计算

`div {width: $var * 10 + 20px;}`

### 4.注释

```scss
/* comment会保留在编译后 */
// comment编译后省略
```

### 5.代码复用

#### MIXIN

`@mixin` 用于定义一个可复用代码块，通过 `@include` 引用，可以指定参数和缺省值

```scss
// 使用@mixin定义代码模块
@mixin left {
    float: left;
}
@mixin prefix($attr, $str) {
    #{$attr}: #{$str};
    -moz-#{$attr}: #{$str};
    -webkit-#{$attr}: #{$str};
}
// 使用@include调用mixin
div {
    @include left;
}
div {
    @include prefix('transform', 'translateX');
}
```

#### `@import`插入文件

`@import '~@/asset/mixin.scss';`

#### 继承

`@extend` 可以从已有选择器继承其他选择器

```scss
.class1 {
    height: 10px;
}
.class2 {
    @extend .class1;
    width: 20px;
}
```

### 7.条件语句

```scss
@if lightness($color) > 30% {
    background-color: #000;
} @else {
    background-color: #fff;
}
```

### 8.循环

常见的循环有`@for`，`@while`，`@each`等

```scss
@for $i from 1 to 10 {
    .border-#{i} {
        border: #{i}px solid #f00;
    }
}
```

### 9.函数

```scss
@function double($n) {
    @return $n * 2;
}
#sidebar {
    width: double(5px);
}
```
