### 概述

![image-20210721155640613](assets\image-20210721155640613.png)

### 优点

![image-20210721155734823](assets\image-20210721155734823.png)

### 下载

![image-20210721155941941](assets\image-20210721155941941.png)

### 入口函数

![image-20210721160224181](assets\image-20210721160224181.png)

### 顶级对象$

![image-20210721160401434](assets\image-20210721160401434.png)

### DOM对象 与 jQuery对象  

![image-20210721160550907](assets\image-20210721160550907.png)

#### 转换

![image-20210721160736329](assets\image-20210721160736329.png)



### jQuery常用API

#### jQuery选择器

![image-20210721161158096](assets\image-20210721161158096.png)

##### jQuery层级选择器

![image-20210721161309085](assets\image-20210721161309085.png)

##### 隐式迭代

![image-20210721161523798](assets\image-20210721161523798.png)

##### 筛选选择器

![image-20210721161556171](assets\image-20210721161556171.png)

##### 筛选方法

![image-20210721161722270](assets\image-20210721161722270.png)

##### 返回指定祖先元素    parents("类名")

```js
// 注意一下都是方法 带括号
        $(function() {
            // 1. 兄弟元素siblings 除了自身元素之外的所有亲兄弟
            $("ol .item").siblings("li").css("color", "red");
            // 2. 第n个元素
            var index = 2;
            // (1) 我们可以利用选择器的方式选择
            // $("ul li:eq(2)").css("color", "blue");
            // $("ul li:eq("+index+")").css("color", "blue");
            // (2) 我们可以利用选择方法的方式选择 更推荐这种写法
            // $("ul li").eq(2).css("color", "blue");
            // $("ul li").eq(index).css("color", "blue");
            // 3. 判断是否有某个类名
            console.log($("div:first").hasClass("current"));
            console.log($("div:last").hasClass("current")); 
        });
```



##### 案例：新浪下拉菜单

```js
        $(function () {
            $(".nav>li").mouseover(function () {
                // 鼠标经过
                $(this).children("ul").show();
            });
            $(".nav>li").mouseout(function () {
                // 鼠标离开
                $(this).children("ul").hide();
            });
        })
```

##### 淘宝精品服饰案例

```js
$(function() {
            // 1. 鼠标经过左侧的小li 
            $("#left li").mouseover(function() {
                // 2. 得到当前小li 的索引号
                var index = $(this).index();
                console.log(index);
                // 3. 让我们右侧的盒子相应索引号的图片显示出来就好了
                // $("#content div").eq(index).show();
                // 4. 让其余的图片（就是其他的兄弟）隐藏起来
                // $("#content div").eq(index).siblings().hide();
                // 链式编程
                $("#content div").eq(index).show().siblings().hide();

            })
        })
```





#### jQuery样式操作

![image-20210721184037320](assets\image-20210721184037320.png)

```js
        // 操作样式之css方法
        $(function() {
            console.log($("div").css("width"));
            // $("div").css("width", "300px");
            // $("div").css("width", 300);
            // $("div").css(height, "300px"); 属性名一定要加引号
            $("div").css({
                width: 400,
                height: 400,
                backgroundColor: "red"
                    // 如果是复合属性则必须采取驼峰命名法，如果值不是数字，则需要加引号
            })
        })
```

##### 类操作

![image-20210722081349727](assets\image-20210722081349727.png)	

##### tab栏切换案例

```js
     $(function() {
            // 1.点击上部的li，当前li 添加current类，其余兄弟移除类
            $(".tab_list li").click(function() {
                // 链式编程操作
                $(this).addClass("current").siblings().removeClass("current");
                // 2.点击的同时，得到当前li 的索引号
                var index = $(this).index();
                console.log(index);
                // 3.让下部里面相应索引号的item显示，其余的item隐藏
                $(".tab_con .item").eq(index).show().siblings().hide();
            });
        })

```

##### 类操作与className的区别

![image-20210722083321234](assets\image-20210722083321234.png)	

#### jQuery效果

jQuery给我们封装了很多动画效果，最常见的如下：

![image-20210722083403174](assets\image-20210722083403174.png)

##### 显示隐藏效果

###### 基本效果

show

hide

toggle

![image-20210722083533593](assets\image-20210722083533593.png)	

###### 滑动效果

slideDown

slideUp

slideToggle

![image-20210722084738488](assets\image-20210722084738488.png)	

![image-20210722084614660](assets\image-20210722084614660.png)	

##### 动画队列

![image-20210722084848001](assets\image-20210722084848001.png)	

```js
$(this).children("ul").stop().slideToggle();
```

##### 淡入淡出

fadeIn

fadeOut

fadeToggle

![image-20210722085133585](assets\image-20210722085133585.png)

​	

fadeTo

![image-20210722085254114](assets\image-20210722085254114.png)	

##### 案例：突出显示

```js
            //鼠标进入的时候,其他的li标签透明度：0.5
            $(".wrap li").hover(function() {
                $(this).siblings().stop().fadeTo(400, 0.5);
            }, function() {
                // 鼠标离开，其他li 透明度改为 1
                $(this).siblings().stop().fadeTo(400, 1);
            })
```

##### 自定义动画

![image-20210722085833571](assets\image-20210722085833571.png)	

```js
$(function() {
            $("button").click(function() {
                $("div").animate({
                    left: 500,
                    top: 300,
                    opacity: .4,
                    width: 500
                }, 500);
            })
        })
```

##### 案例：手风琴效果

```js
            $(function () {
                // 鼠标经过某个li 有两步操作
                $(".king li").mouseenter(function () {
                    // 当前li 宽度变为224px 小图片淡出 大图片淡入
                    $(this).stop().animate({
                        width: 224
                    }).find(".small").stop().fadeOut().siblings(".big").stop().fadeIn();
                    // 其余兄弟li宽度变为69px  小图片淡入  大图片淡出
                    $(this).siblings().stop().animate({
                        width: 69
                    }).find(".small").stop().fadeIn().siblings(".big").stop().fadeOut();
                })
            });
```



#### jQuery属性操作

##### prop

![image-20210722094006907](assets\image-20210722094006907.png)

##### attr	

![image-20210722093637508](assets\image-20210722093637508.png)	

##### 数据缓存 date

![image-20210722094352468](assets\image-20210722094352468.png)	

```html
    <a href="http://www.itcast.cn" title="都挺好">都挺好</a>
    <input type="checkbox" name="" id="" checked>
    <div index="1" data-index="2">我是div</div>
    <span>123</span>
    <script>
        $(function() {
            //1. element.prop("属性名") 获取元素固有的属性值
            console.log($("a").prop("href"));
            $("a").prop("title", "我们都挺好");
            $("input").change(function() {
                console.log($(this).prop("checked"));

            });
            // console.log($("div").prop("index"));
            // 2. 元素的自定义属性 我们通过 attr()
            console.log($("div").attr("index"));
            $("div").attr("index", 4);
            console.log($("div").attr("data-index"));
            // 3. 数据缓存 data() 这个里面的数据是存放在元素的内存里面
            $("span").data("uname", "andy");
            console.log($("span").data("uname"));
            // 这个方法获取data-index h5自定义属性 第一个 不用写data-  而且返回的是数字型
            console.log($("div").data("index"));
        })
    </script>
```

##### 案例：购物车模块

```js
    // 2. 如果小复选框被选中的个数等于3 就应该把全选按钮选上，否则全选按钮不选。
    $(".j-checkbox").change(function() {
        // if(被选中的小的复选框的个数 === 3) {
        //     就要选中全选按钮
        // } else {
        //     不要选中全选按钮
        // }
        // console.log($(".j-checkbox:checked").length);
        // $(".j-checkbox").length 这个是所有的小复选框的个数
        if ($(".j-checkbox:checked").length === $(".j-checkbox").length) {
            $(".checkall").prop("checked", true);
        } else {
            $(".checkall").prop("checked", false);
        }
```



#### jQuery文本属性值

##### 内容文本值

```js
        // 1. 获取设置元素内容 html()
        console.log($("div").html());
        // $("div").html("123");
        // 2. 获取设置元素文本内容 text()
        console.log($("div").text());
        $("div").text("123");

        // 3. 获取设置表单值 val()
        console.log($("input").val());
        $("input").val("123");
```

###### 案例：增加商品数量模块 修改商品小计

```js
    // 3. 增减商品数量模块 首先声明一个变量，当我们点击+号（increment），就让这个值++，然后赋值给文本框。
    $(".increment").click(function() {
        // 得到当前兄弟文本框的值
        var n = $(this).siblings(".itxt").val();
        // console.log(n);
        n++;
        $(this).siblings(".itxt").val(n);
        // 3. 计算小计模块 根据文本框的值 乘以 当前商品的价格  就是 商品的小计
        // 当前商品的价格 p  
        var p = $(this).parents(".p-num").siblings(".p-price").html();
        // console.log(p);
        p = p.substr(1);
        console.log(p);
        var price = (p * n).toFixed(2);
        // 小计模块 
        // toFixed(2) 可以让我们保留2位小数
        $(this).parents(".p-num").siblings(".p-sum").html("￥" + price);
        getSum();
    });
```

###### toFixed(数字)  保留几位小数

```js
    //  4. 用户修改文本框的值 计算 小计模块  
    $(".itxt").change(function() {
        // 先得到文本框的里面的值 乘以 当前商品的单价 
        var n = $(this).val();
        // 当前商品的单价
        var p = $(this).parents(".p-num").siblings(".p-price").html();
        // console.log(p);
        p = p.substr(1);
        $(this).parents(".p-num").siblings(".p-sum").html("￥" + (p * n).toFixed(2));
        getSum();
    });

```



#### jQuery元素操作

##### 遍历元素

![image-20210722104234439](assets\image-20210722104234439.png)	

```js
            var arr = ["red", "green", "blue"];
            $("div").each(function(i, domEle) {
                // 回调函数第一个参数一定是索引号  可以自己指定索引号号名称
                // console.log(index);
                // console.log(i);
                // 回调函数第二个参数一定是 dom元素对象 也是自己命名
                // console.log(domEle);
                // domEle.css("color"); dom对象没有css方法
                $(domEle).css("color", arr[i]);
```

![image-20210722105110746](assets\image-20210722105110746.png)	

```js
            // 2. $.each() 方法遍历元素 主要用于遍历数据，处理数据
            $.each($("div"), function(i, ele) {
                console.log(i);
                console.log(ele);
            });
```

```js
            $.each(arr, function(i, ele) {
                console.log(i);
                console.log(ele);
            })
```

```js
            $.each({
                name: "andy",
                age: 18
            }, function (i, ele) {
                console.log(i); // 输出的是 name age 属性名
                console.log(ele); // 输出的是 andy  18 属性值
            })
```

##### 案例：计算总计和总额

```js
getSum();
function getSum() {
        var count = 0; // 计算总件数 
        var money = 0; // 计算总价钱
        $(".itxt").each(function(i, ele) {
            count += parseInt($(ele).val());
        });
        $(".amount-sum em").text(count);
        $(".p-sum").each(function(i, ele) {
            money += parseFloat($(ele).text().substr(1));
        });
        $(".price-sum em").text("￥" + money.toFixed(2));
    }
```

案例：购物车js代码

```js
$(function() {
    // 1. 全选 全不选功能模块
    // 就是把全选按钮（checkall）的状态赋值给 三个小的按钮（j-checkbox）就可以了
    // 事件可以使用change
    $(".checkall").change(function() {
        // console.log($(this).prop("checked"));
        $(".j-checkbox, .checkall").prop("checked", $(this).prop("checked"));
        if ($(this).prop("checked")) {
            // 让所有的商品添加 check-cart-item 类名
            $(".cart-item").addClass("check-cart-item");
        } else {
            // check-cart-item 移除
            $(".cart-item").removeClass("check-cart-item");
        }
    });
    // 2. 如果小复选框被选中的个数等于3 就应该把全选按钮选上，否则全选按钮不选。
    $(".j-checkbox").change(function() {
        // if(被选中的小的复选框的个数 === 3) {
        //     就要选中全选按钮
        // } else {
        //     不要选中全选按钮
        // }
        // console.log($(".j-checkbox:checked").length);
        // $(".j-checkbox").length 这个是所有的小复选框的个数
        if ($(".j-checkbox:checked").length === $(".j-checkbox").length) {
            $(".checkall").prop("checked", true);
        } else {
            $(".checkall").prop("checked", false);
        }
        if ($(this).prop("checked")) {
            // 让当前的商品添加 check-cart-item 类名
            $(this).parents(".cart-item").addClass("check-cart-item");
        } else {
            // check-cart-item 移除
            $(this).parents(".cart-item").removeClass("check-cart-item");
        }
    });
    // 3. 增减商品数量模块 首先声明一个变量，当我们点击+号（increment），就让这个值++，然后赋值给文本框。
    $(".increment").click(function() {
        // 得到当前兄弟文本框的值
        var n = $(this).siblings(".itxt").val();
        // console.log(n);
        n++;
        $(this).siblings(".itxt").val(n);
        // 3. 计算小计模块 根据文本框的值 乘以 当前商品的价格  就是 商品的小计
        // 当前商品的价格 p  
        var p = $(this).parents(".p-num").siblings(".p-price").html();
        // console.log(p);
        p = p.substr(1);
        console.log(p);
        var price = (p * n).toFixed(2);
        // 小计模块 
        // toFixed(2) 可以让我们保留2位小数
        $(this).parents(".p-num").siblings(".p-sum").html("￥" + price);
        getSum();
    });
    $(".decrement").click(function() {
        // 得到当前兄弟文本框的值
        var n = $(this).siblings(".itxt").val();
        if (n == 1) {
            return false;
        }
        // console.log(n);
        n--;
        $(this).siblings(".itxt").val(n);
        // var p = $(this).parent().parent().siblings(".p-price").html();
        // parents(".p-num") 返回指定的祖先元素
        var p = $(this).parents(".p-num").siblings(".p-price").html();
        // console.log(p);
        p = p.substr(1);
        console.log(p);
        // 小计模块 
        $(this).parents(".p-num").siblings(".p-sum").html("￥" + (p * n).toFixed(2));
        getSum();
    });
    //  4. 用户修改文本框的值 计算 小计模块  
    $(".itxt").change(function() {
        // 先得到文本框的里面的值 乘以 当前商品的单价 
        var n = $(this).val();
        // 当前商品的单价
        var p = $(this).parents(".p-num").siblings(".p-price").html();
        // console.log(p);
        p = p.substr(1);
        $(this).parents(".p-num").siblings(".p-sum").html("￥" + (p * n).toFixed(2));
        getSum();
    });
    // 5. 计算总计和总额模块
    getSum();

    function getSum() {
        var count = 0; // 计算总件数 
        var money = 0; // 计算总价钱
        $(".itxt").each(function(i, ele) {
            count += parseInt($(ele).val());
        });
        $(".amount-sum em").text(count);
        $(".p-sum").each(function(i, ele) {
            money += parseFloat($(ele).text().substr(1));
        });
        $(".price-sum em").text("￥" + money.toFixed(2));
    }
    // 6. 删除商品模块
    // (1) 商品后面的删除按钮
    $(".p-action a").click(function() {
        // 删除的是当前的商品 
        $(this).parents(".cart-item").remove();
        getSum();
    });
    // (2) 删除选中的商品
    $(".remove-batch").click(function() {
        // 删除的是小的复选框选中的商品
        $(".j-checkbox:checked").parents(".cart-item").remove();
        getSum();
    });
    // (3) 清空购物车 删除全部商品
    $(".clear-all").click(function() {
        $(".cart-item").remove();
        getSum();
    })
})
```



#### jQuery尺寸、位置操作

##### 尺寸方法

![image-20210722113119347](assets\image-20210722113119347.png)	

##### 位置操作

###### offset()

![image-20210722113537261](assets\image-20210722113537261.png)	

###### position()

![image-20210722113756895](assets\image-20210722113756895.png)	

###### srollTop()/scrollLeft()

```js
        $(function() {
            $(document).scrollTop(100);
            // 被卷去的头部 scrollTop()  / 被卷去的左侧 scrollLeft()
            // 页面滚动事件
            var boxTop = $(".container").offset().top;
            $(window).scroll(function() {
                // console.log(11);
                console.log($(document).scrollTop());
                if ($(document).scrollTop() >= boxTop) {
                    $(".back").fadeIn();
                } else {
                    $(".back").fadeOut();
                }
            });
            // 返回顶部
            $(".back").click(function() {
                // $(document).scrollTop(0);
                $("body, html").stop().animate({
                    scrollTop: 0
                });
                // $(document).stop().animate({
                //     scrollTop: 0
                // }); 不能是文档而是 html和body元素做动画
            })
        })
```

###### 电梯导航案例

```js
$(function() {
    // 当我们点击了小li 此时不需要执行 页面滚动事件里面的 li 的背景选择 添加 current
    // 节流阀  互斥锁 
    var flag = true;
    // 1.显示隐藏电梯导航
    var toolTop = $(".recommend").offset().top;
    toggleTool();

    function toggleTool() {
        if ($(document).scrollTop() >= toolTop) {
            $(".fixedtool").fadeIn();
        } else {
            $(".fixedtool").fadeOut();
        };
    }

    $(window).scroll(function() {
        toggleTool();
        // 3. 页面滚动到某个内容区域，左侧电梯导航小li相应添加和删除current类名


        if (flag) {
            $(".floor .w").each(function(i, ele) {
                if ($(document).scrollTop() >= $(ele).offset().top) {
                    console.log(i);
                    $(".fixedtool li").eq(i).addClass("current").siblings().removeClass();

                }
            })
        }



    });
    // 2. 点击电梯导航页面可以滚动到相应内容区域
    $(".fixedtool li").click(function() {
        flag = false;
        console.log($(this).index());
        // 当我们每次点击小li 就需要计算出页面要去往的位置 
        // 选出对应索引号的内容区的盒子 计算它的.offset().top
        var current = $(".floor .w").eq($(this).index()).offset().top;
        // 页面动画滚动效果
        $("body, html").stop().animate({
            scrollTop: current
        }, function() {
            flag = true;
        });
        // 点击之后，让当前的小li 添加current 类名 ，姐妹移除current类名
        $(this).addClass("current").siblings().removeClass();
    })
})
```



### jQuery事件

#### 事件注册

```js
            //1. 单个事件注册
            $("div").click(function() {
                $(this).css("background", "purple");
            });
            $("div").mouseenter(function() {
                $(this).css("background", "skyblue");
            });
```

#### 事件处理

##### 事件处理on	

```js
           // 2. 事件处理on
              //  (1) on可以绑定1个或者多个事件处理程序
            $("div").on({
                mouseenter: function () {
                    $(this).css("background", "skyblue");
                },
                click: function () {
                    $(this).css("background", "purple");
                },
                mouseleave: function () {
                    $(this).css("background", "blue");
                }
            });
            $("div").on("mouseenter mouseleave", function () {
                $(this).toggleClass("current");
            });
```

##### 优势1

![image-20210722132511196](assets\image-20210722132511196.png)	

##### 优势2事件委派

![image-20210722132902112](assets\image-20210722132902112.png)	

##### 优势3 动态创建元素

![image-20210722133147171](assets\image-20210722133147171.png)	

```js
 		$(function () {
            // 1. 单个事件注册
            // $("div").click(function () {
            //     $(this).css("background", "purple");
            // });
            // $("div").mouseenter(function () {
            //     $(this).css("background", "skyblue");
            // });

            2. 事件处理on
                (1) on可以绑定1个或者多个事件处理程序
            $("div").on({
                mouseenter: function () {
                    $(this).css("background", "skyblue");
                },
                click: function () {
                    $(this).css("background", "purple");
                },
                mouseleave: function () {
                    $(this).css("background", "blue");
                }
            });
            $("div").on("mouseenter mouseleave", function () {
                $(this).toggleClass("current");
            });
            // (2) on可以实现事件委托（委派）
            // $("ul li").click();
            $("ul").on("click", "li", function () {
                alert(11);
            });
            // click 是绑定在ul 身上的，但是 触发的对象是 ul 里面的小li
            // (3) on可以给未来动态创建的元素绑定事件
            // $("ol li").click(function() {
            //     alert(11);
            // })
            $("ol").on("click", "li", function () {
                alert(11);
            })
            var li = $("<li>我是后来创建的</li>");
            $("ol").append(li);
        })
```



##### 案例：发布微博案例

```html
    <script>
        $(function() {
            // 1.点击发布按钮， 动态创建一个小li，放入文本框的内容和删除按钮， 并且添加到ul 中
            $(".btn").on("click", function() {
                var li = $("<li></li>");
                li.html($(".txt").val() + "<a href='javascript:;'> 删除</a>");
                $("ul").prepend(li);
                li.slideDown();
                $(".txt").val("");
            })

            // 2.点击的删除按钮，可以删除当前的微博留言li
            // $("ul a").click(function() {  // 此时的click不能给动态创建的a添加事件
            //     alert(11);
            // })
            // on可以给动态创建的元素绑定事件
            $("ul").on("click", "a", function() {
                $(this).parent().slideUp(function() {
                    $(this).remove();
                });
            })

        })
    </script>
```



##### 事件解绑off

![image-20210722134151352](assets\image-20210722134151352.png)	

```js
        $(function() {
            $("div").on({
                click: function() {
                    console.log("我点击了");
                },
                mouseover: function() {
                    console.log('我鼠标经过了');
                }
            });
            $("ul").on("click", "li", function() {
                alert(11);
            });
            // 1. 事件解绑 off 
            // $("div").off();  // 这个是解除了div身上的所有事件
            $("div").off("click"); // 这个是解除了div身上的点击事件
            $("ul").off("click", "li");
            // 2. one() 但是它只能触发事件一次
            $("p").one("click", function() {
                alert(11);
            })
        })
```



##### 自动触发事件

![image-20210722134321520](assets\image-20210722134321520.png)	

```js
        $(function() {
            $("div").on("click", function() {
                alert(11);
            });

            // 自动触发事件
            // 1. 元素.事件()
            // $("div").click();会触发元素的默认行为
            // 2. 元素.trigger("事件")
            // $("div").trigger("click");会触发元素的默认行为
            $("input").trigger("focus");
            // 3. 元素.triggerHandler("事件") 就是不会触发元素的默认行为
            $("div").triggerHandler("click");
            $("input").on("focus", function() {
                $(this).val("你好吗");
            });
            // $("input").triggerHandler("focus");

        });
```



#### 事件对象

 阻止冒泡![image-20210722135001946](assets\image-20210722135001946.png)	

### jQuery对象拷贝

![image-20210722135152953](assets\image-20210722135152953.png)	

###  jQuery多库共存

![image-20210722135643751](assets\image-20210722135643751.png)	

### jQuery插件

![image-20210722135759579](assets\image-20210722135759579.png)	

#### 图片懒加载

#### 全屏滚动

![image-20210722140700082](assets\image-20210722140700082.png)		

### bootstrap组件

















