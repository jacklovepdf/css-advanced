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
