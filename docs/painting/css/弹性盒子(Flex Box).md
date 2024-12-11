# 弹性盒子（Flex Box）

??? "display: -webkit-flex 与 display: flex"

    1. **`display: -webkit-flex;`**

        - `-webkit-` 是一个**厂商前缀**，表示这是一个为支持旧版本 WebKit 内核的浏览器（如旧版 Chrome 和 Safari）添加的兼容性声明。
        - 在早期版本的 WebKit 浏览器中，`flexbox` 是通过 `-webkit-flex` 实现的。新版本的浏览器已经不需要这个前缀。

    2. **`display: flex;`**
        - 这是标准的 CSS 声明，适用于大多数现代浏览器，包括最新版本的 Chrome、Firefox、Safari、Edge 和 Opera。
        - 不依赖厂商前缀，更符合当前的 Web 开发规范。

    3. **为什么同时使用两个声明？**
        为了兼容性。如果需要支持较旧版本的浏览器（例如老版 Safari 或 Android 浏览器），可以先写带前缀的版本（`-webkit-flex`），再写标准的版本（`flex`）。浏览器会选择支持的那个。
        例如：
        ```css
        .my-container {
        display: -webkit-flex; /* 兼容旧版 WebKit 浏览器 */
        display: flex; /* 现代浏览器支持 */
        }
        ```

## 一、Flex 布局是什么？

Flex 是 Flexible Box 的缩写，意为”弹性布局”，用来为盒状模型提供最大的灵活性。

任何一个容器都可以指定为 Flex 布局。

```css
.box {
  display: flex;
}
```

行内元素也可以使用 Flex 布局。

```css
.box {
  display: inline-flex;
}
```

Webkit 内核的浏览器，必须加上-webkit 前缀。

```css
.box{
display: -webkit-flex; /_ Safari _/
display: flex;
}
```

!!! warning

    注意，设为 Flex 布局以后，子元素的 float、clear 和 vertical-align 属性将失效。

## Flex 容器相关属性

### display

### flex-direction

### flex-wrap

### flex-flow

### justify-content
