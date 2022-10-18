1. 设置div背景图片，按照一定比例自适应展示

```css
position: relative;
width: 100%;
height: 0;
padding-top: 75%;
transform-origin: top;
background: url(${props => props.bgUrl});
background-size: cover;
z-index: 50;
```

2.Flex布局

```css
display: flex;
flex-direction: row;
align-items: center; // 垂直居中
flex: 1;
justify-content: space-around; // center:水平居中
```

3.图标与文字并排，对齐顶部

```css
vertical-align: top;
```

4.给div表面增加一层遮罩

```css
.filter {
  position: absolute;
  top: 0;
  left: 0;
  width: 100%;
  height: 100%;
  background: rgba(7, 17, 27, 0.3);
}
```

5.绝对定位居中(所居中的div已知高度和宽度)

```css
position: absolute;
left: 0; right: 0;
margin: auto;
```

6.图片变大

```css
imageWrapperDom.style.transform = `scale(${1 + percent})`;
```

7.绝对定位元素跟随移动  translate3d(x, y, z)

```css
collectButtonDom.style.transform = `translate3d(0, ${newY}px, 0)`;
```

