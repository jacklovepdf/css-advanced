# css-advanced
some tips and experience to css;


## Table of Contents

- [css std and compatibility](#accustoming-yourself-to-javascript)
- [css code standards](#variable-scope)

## css std and compatibility

1.css回退机制。
    
    css提供回退机制是一种必要的手段，它可以确保web应用在应对浏览器兼容性问题时候不至于挂掉，只是可能没有那么炫酷而已；
常见几种提供回退样式的方法
    
（1）样式声明的层叠机制
   比如为不支持渐变的浏览器提供纯色的背景；

```css
    background: rgb(255, 128, 0); //提供回退机制
    background: -moz-linear-gradient(0deg, yellow, red); //
    background: -o-linear-gradient(0deg, yellow, red);
    background: -webkit-linear-gradient(0deg, yellow, red);
    background: linear-gradient(90deg, yellow, red); //浏览器兼容写法，标准写法写在最后
```

（2）modernizr给根元素提供辅助类；

```css
    h1 { color: gray; }
    .textshadow h1 {
    color: transparent; text-shadow: 0 0 .3em gray;
    }
```

（3）自己编写js代码进行特性检测，给根元素添加一些辅助类；

```javascript
    //检测浏览器是否支持相关特性；
    function testProperty(property) {
        var root = document.documentElement;
        if (property in root.style) {
            root.classList.add(property.toLowerCase());
            return true;
        }else{
            root.classList.add('no-' + property.toLowerCase());
            return false;
        }
    }
```

```javascript
    //检测浏览器特性是否支持相关值；
    function testValue(id, value, property) {
        var dummy = document.createElement('p');
        dummy.style[property] = value;
        if (dummy.style[property]) {
            root.classList.add(id);
            return true;
        }else{
            root.classList.add('no-' + id);
            return false;
        }
    }
```

**Note**: 浏览器在解析css代码的时候，总是会丢弃无法识别的部分，因此，我们可以给元素动态的添加样式，通过查看它是否生效来检测浏览器
是否支持相关的特性；

## css code standards

1. css编码规范

   对于任何软件开发来说，保持代码可复用以及可维护是最大的挑战之一；


1.1 响应式网页设计

使用百分比长度来取代固定长度。如果实在做不到这一点，也应该 尝试使用与视口相关的单位(vw、vh、vmin 和 vmax)，它们的值解析为视口宽度或高度的百分比。
(1)当你需要在较大分辨率下得到固定宽度时，使用 max-width 而不是 width，因为它可以适应较小的分辨率，而无需使用媒体查询。
(2)不要忘记为**替换元素**(比如 img、object、video、iframe 等)设置一个max-width，值为 100%。
(3)假如背景图片需要完整地铺满一个容器，不管容器的尺寸如何变化， background-size: cover 这个属性都可以做到。但是，我们也要时刻牢记——带宽并不是无限的，因此在移动网页中通过CSS把一张大图缩小显示往往是不太明智的。
(4)当图片(或其他元素)以行列式进行布局时，让视口的宽度来决定列的数量。弹性盒布局(即 Flexbox)或者 display: inline-block加上常规的文本折行行为，都可以实现这一点。
(5)在使用多列文本时，指定column-width(列宽)而不是指定 column-count(列数)，这样它就可以在较小的屏幕上自动显示为单列布局。
(6)媒体查询中使用em或者rem来替换固定单位（eg px）

**Note:**响应式布局实际上并不需要过多的媒体查询，尽可能实现弹性可伸缩的布局，并在媒体查询的各个断点区间内指定相应的尺寸。
这意味着媒体查询只是把一些外边距收拢到最小程度，然后把因为屏幕太窄而无法显示成双列的侧栏调整为单列布局而已

1.2 合理使用简写

```javascript
    background: url(tr.png) top right, url(br.png) bottom right,
                url(bl.png) bottom left;
    background-size: 2em 2em;
    background-repeat: no-repeat;
```

1.3 关于使用css预处理器

优点：


缺点：
    css文件体积和复杂的不可控；
    增加调试难度（通过sourcemap可以缓解）；
    增加开发过程中的延时；
    抽象会带来更高的学习成本；


3.背景和边框

3.1 半透明边框

(1) background-clip 属性规定背景的绘制区域。
    | 属性值        | 含义                   |
    | --------     | -----:                |
    | border-box   | 背景被裁剪到边框盒。     |
    | padding-box  | 背景被裁剪到内边距框。   |
    | content-box  | 背景被裁剪到内容框。     |

3.2 多重边框

(1) box-shadow 属性向框添加一个或多个阴影。
    box-shadow: h-shadow v-shadow blur spread color inset;




3.3


4.形状


5.视觉效果

