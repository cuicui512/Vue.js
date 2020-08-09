

## Vue.js快速入门

1. 教程地址：[黑马程序员](https://www.bilibili.com/video/BV12J411m7MG?from=search&seid=6932484561214481070)
2. 学前须知：HTML，JavaScript，Css，AJAX
3. 开发工具：
   - Vscode
   - Live Server (插件功能：代码保存时，浏览器自动刷新页面，使用时在Vscode中右键以插件打开HTML)   
4. 课程安排：①Vue基础   ②本地应用   ③网络应用   ④综合应用
5. [Vue.js官方参考文档](https://cn.vuejs.org/v2/guide/)

### 小技巧

1. Vscode新建html时，！+Tab 即可生成模板 

2. <script>标签中（JavaScript），用逗号分割元素，元素中间不可缺少
   <span> 用于对文档中的行内元素进行组合,用于对文本着色

3. 外层有双引号时，内层只能用单引号

### 一、Vue 基础



#### Vue简介

- **基于 JavaScript 的框架**	 

- 简化 *Dom* 操作	 

- *响应式*  数据驱动

  ------

#### 第一个Vue程序



- 导入*开发版本*的Vue.js
- 创建Vue实例对象，设置*el*属性和*data*属性
- 实用简洁的*模板语法*把数据渲染到页面上

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>第一个Vue程序</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">
        {{message}}
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{      // data 是数据对象
                message:"Hello Vue!"
            }
         })
    </script>
</body>
</html>
```



#### el：挂载点

​	**作用**：el是用来设置Vue实例挂载（管理）的元素

1. Vue实例的作用范围？

   ​	Vue会管理el选项*命中的与元素*及其内部的*后代元素*

2. 是否可以使用其他选择器？

   ​	可以使用其他的选择器（class,div),但是建议使用*id选择器*

3. 是否可以设置其他的dom元素？

   ​	可以使用其他的双标签，*除了<html>和<body>*

```html
<script>
         var app = new Vue({
            el:"#app",
             //el:".app",    // .是class选择器
            //el:"div",       //div 选择器
            data:{
             message:" 黑马程序员"
         }
       })
    </script>
```



#### data:数据对象

- Vue中用到的数据定义在*data*中

- data中可以写*复杂类型*的数据

- 渲染复杂数据类型时，遵守*js的语法*即可

  ```html
  <!DOCTYPE html>
  <html lang="en">
  <head>
      <meta charset="UTF-8">
      <meta name="viewport" content="width=device-width, initial-scale=1.0">
      <title>data:数据对象</title>
  </head>
  <body>
      <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
      <div id="app">
          {{message}}
          <h2> {{school.name}} {{school.mobile_phone}}</h2>
          <ul>
              <li>{{campus[0]}}</li>
              <li>{{campus[1]}}</li>
          </ul>
      </div>
  
      <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
      <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
      
      <!-- 创建Vue实例对象，设置el和data属性 -->
      <script>
       var app = new Vue({
             el:"#app",
             data:{
                  message:" 你好 XDUer！",
                  school:{
                      name:"XDUer",
                      mobile_phone:"100000"
                   },
                   campus:["长安","雁塔"]   // 数组元素类型
              }
           })
      </script>
  </body>
  </html>
  ```





### 二、本地应用

- 通过*Vue*实现常见的网页效果
- 学习*Vue指令*，以案例巩固知识点
- Vue指令指的是，以 *v-* 开头的一组特殊语法

 

#### v-text 指令

**作用**：设置标签的文本值（textContext)

默认写法会替换全部内容，使用*差值表达式{{}}*可以替换指定内容

内部支持写*表达式*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-text 指令</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">  
        <h2 v-text="message+'！'">西安</h2>    <!-- v-text标签会直接替换所有的文本内容，西安不会显示 -->
        <h2 v-text="info">西安</h2>
        <h2>{{message + "!"}}西安</h2>        <!-- {{ }} 只直接替换部分的的文本内容，西安会显示 -->
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{      // data 是数据对象
                message:"Hello Vue",
                info: "Vue标签指令"
            }
         })
    </script>
</body>
</html>
```



#### v-html 指令

**作用**：设置标签的innerHTML

- 内容中有*html结构*会被解析为*标签*，没有时同v-text指令一样
- v-text指令无论内容，只会解析为*文本*
- *解析文本*使用v-text，*解析html结构*使用v-html

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v- 指令</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">  
        <p v-html="content"></p> 
        <p v-text="content"></p>     
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{      // data 是数据对象
                // content: "个人博客"
                content:"<a href='http://www.lxblog.club'>个人博客</a>"
            }
         })
    </script>
</body>
</html>
```



#### v-on 指令

**作用**：为元素绑定事件

- 事件名不需要写*on*
- 指令可以简写为*@*
- 绑定的方法定义在*methods*属性中
- 方法内部通过*this关键字*可以访问定义在*data*中的数据

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v- 指令</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">  
        <input type="button" value="v-on指令" v-on:click="doIt">  
        <input type="button" value="v-on指令简写" @click="doIt">
        <input type="button" value="v-on双击指令" @dblclick="doIt"> 
        <h2 @click="changefood">{{food}}</h2>    <!-- 点击调用changefood函数 -->
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{
                food:"粗粗香扒饭"
            },
            methods:{
                doIt:function(){
                    alert("done");
                },
                changefood:function(){  //通过this关键字拿到data内部的数据
                    this.food+="好好吃！"   //调用一次函数，food后面加一个好好吃
                }
            }
         })
    </script>
</body>
</html>
```

#### 计数器

1. data中定义数据，比如num
2. methods中添加两个方法，add(递增)，sub(递减)
3. 使用v-text将num设置给span标签
4. 使用v-on将add,sub分别绑定给+，- 按钮
5. 递增（减）逻辑判断：大于10（小于0）给出提示

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>计数器</title>
    <link rel="stylesheet" href="index.css">
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">
        <div class="input-num">
            <button @click="sub">-</button>
            <span v-text="num"></span>
            <button @click="add">+</button>
        </div>
        <img src="http://www.itheima.com/images/logo.png"/>
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{
                num:0
            },
            methods:{
                // add递增函数
                add:function(){  //通过this关键字拿到data内部的数据
                    if(this.num<10){
                        //console.log("add")  //浏览器，f12,控制台
                        this.num++
                    }
                    else
                    alert("达到最大值10！")
                },
                // sub递减函数
                sub:function(){  //通过this关键字拿到data内部的数据
                    if(this.num>0){
                        //console.log("sub")  //浏览器，f12, Console控制台
                        this.num--
                    }
                    else
                    alert("达到最小值0！" ) 
                }
            }
         })
    </script>
</body>
</html>
```

```css
body{
    background-color: #f5f5f5;
  }
  #app {
    width: 480px;
    height: 80px;
    margin: 200px auto;
  }
  .input-num {
    margin-top:20px;
    height: 100%;
    display: flex;
    border-radius: 10px;
    overflow: hidden;
    box-shadow: 4px 4px 4px #adadad;
    border: 1px solid #c7c7c7;
    background-color: #c7c7c7;
  }
  .input-num button {
    width: 150px;
    height: 100%;
    font-size: 40px;
    color: #ad2a27;
    cursor: pointer;
    border: none;
    outline: none;
    background-color:rgba(0, 0, 0, 0);
  }
  .input-num span {
    height: 100%;
    font-size: 40px;
    flex: 1;
    text-align: center;
    line-height: 80px;
    font-family:auto;
    background-color: white;
  }
  img{
    float: right;
    margin-top: 50px;
  }
```



#### v-show 指令

**作用**：根据表达式值的真假，切换元素的显示和隐藏

- *v-show*的原理是修改元素的display,实现元素的显示/隐藏
- 指令后面的内容，最终都会解析为*布尔值*
- 值为*true*元素显示，值为*false*元素隐藏
- 数据改变之后，对应元素的显示状态会*同步更新*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-show 指令</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">
        <input type="button" value="切换显示状态" @click="change_isShow" > 
        <img v-show="isShow" src="ear_phone.jpg" alt="">
        <img v-show="age>18" src="ear_phone.jpg" alt="">     <!-- 当age不满足条件时第二张图不会显示出来，可以通过定义函数改变age的值 -->   
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data: {      // data 是数据对象
               isShow:false,
               age:17
            },
            methods: {
                change_isShow:function(){ 
                    this.isShow = !this.isShow ;               
                }
            }
         })
    </script>
</body>
</html>

```



#### v-if 指令

**作用**：根据表达式值的真假，切换元素的显示和隐藏（操纵dom元素）

- v-if本质是通过*操纵dom元素*来切换状态
- 表达式的值为*true*，元素存在于dom树中，值为*false*，元素从dom树中移除
- 频繁的切换时使用v-show,反之使用v-if，因为*v-show的切换消耗较小*

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-if 指令</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">
        <h2 v-if="temperature>=35">temperature>35啦</h2>
        <p v-if="isShow">xidian university</p>      <!-- v-if是将当前的dom(<p>标签)直接注释掉 -->
        <p v-show="isShow">xidian university   v-show</p>   <!-- v-show是将当前的dom(<p>标签)里面的display属性改变 -->
        <input type="button" value="切换显示" @click="change_isShow">
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data: {      // data 是数据对象
               isShow:false,
               temperature:40
            },
            methods: {
                change_isShow:function(){ 
                    this.isShow = !this.isShow ;               
                }
            }
         })
    </script>
</body>
</html>
```





#### v-bind 指令

**作用**：设置元素的属性（例如：title,src,class等）

- 完整写法： *v-bind:属性名*
- 简写：*：属性名*
- 需要动态的增删*class*建议使用对象的方式

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-bind 指令</title>
</head>

<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">
        <img v-bind:src="imgSrc" alt="" v-bind:title="imgTitle">
        <img :src="imgSrc1" alt="" :title="imgTitle + '!'" >   <!-- 简写,支持字符串拼接 -->
    </div>    
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{      // data 是数据对象
                imgSrc:"https://i.ytimg.com/vi/WzLqZ9Rz4RU/hqdefault.jpg",
                imgSrc1:"http://www.itheima.com/images/logo.png",
                imgTitle:"This is a picture!"
            }
         })
    </script>
</body>
</html>

```



#### 图片切换

1. 定义图片数组	imgArr[]
2. 添加图片索引	index
3. 绑定src属性 	imgArr[index]
4. 图片切换逻辑 	methods方法中改变索引即可
5. 显示状态切换 	v-show 消耗小一些

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-bind 指令</title>
    <link rel="stylesheet" href="picture.css" />
</head>

<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="mask">
        <div class="center">
            <img :src="imgArr[index]">
            <!--左箭头图标-->
            <a href="javascript:void(0)" class="left" v-if="index!=0" @click="prev">
                <img src="https://yt3.ggpht.com/a/AATXAJxeVjUdPfVKFJ7aluzMwCUJCftmjrWQeh691Q=s48-c-k-c0xffffffff-no-rj-mo" > 
            </a> 
            <!--右箭头图标-->
            <a href="javascript:void(0)" class="right"  v-show="index<imgArr.length-1" @click="next">
                <img src="https://yt3.ggpht.com/a/AATXAJy1e4K9Dc136juXzai6dSai9SNGVuw6AmXVuIwH=s48-c-k-c0xffffffff-no-rj-mo"> 
            </a> 
        </div>
    </div>    
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var mask =new Vue({
            el:"#mask",  // el 是挂载点 ; # 是id选择器
            data:{      // data 是数据对象
                imgArr:[    // 图片数组
                     "https://i.ytimg.com/vi/WzLqZ9Rz4RU/hqdefault.jpg",
                     "http://www.itheima.com/images/logo.png",
                     "https://lh3.googleusercontent.com/a-/AOh14GgSljZFc6oObsXig07LbETN9kUZYs--XY27gVB2=s88",
                     "https://yt3.ggpht.com/a/AATXAJyMtUMPxrW58lb-2BhNyl6tgAqHXfJQ1Utap792=s88-c-k-c0xffffffff-no-rj-mo"
                 ],
                index:0  // 图片索引
            },
            methods:{
                prev:function(){    //  前一页函数
                    this.index--;
                },
                next:function(){    // 后一页函数
                    this.index++;
                }
             }
         })
    </script>
</body>
</html>

```

```css
* {
    margin: 0;
    padding: 0;
  }
  
  html,
  body,
  #mask {
    width: 100%;
    height: 100%;
  }
  
  #mask {
    background-color: #c9c9c9;
    position: relative;
  }
  
  #mask .center {
    position: absolute;
    background-color: #fff;
    left: 50%;
    top: 50%;
    transform: translate(-50%, -50%);
    padding: 10px;
  }
  #mask .center .title {
    position: absolute;
    display: flex;
    align-items: center;
    height: 56px;
    top: -61px;
    left: 0;
    padding: 5px;
    padding-left: 10px;
    padding-bottom: 0;
    color: rgba(175, 47, 47, 0.8);
    font-size: 26px;
    font-weight: normal;
    background-color: white;
    padding-right: 50px;
    z-index: 2;
  }
  #mask .center .title img {
    height: 40px;
    margin-right: 10px;
  }
  
  #mask .center .title::before {
    content: "";
    position: absolute;
    width: 0;
    height: 0;
    border: 65px solid;
    border-color: transparent transparent white;
    top: -65px;
    right: -65px;
    z-index: 1;
  }
  
  #mask .center > img {
    display: block;
    width: 700px;
    height: 458px;
  }
  
  #mask .center a {
    text-decoration: none;
    width: 45px;
    height: 100px;
    position: absolute;
    top: 179px;
    vertical-align: middle;
    opacity: 0.5;
  }
  #mask .center a :hover {
    opacity: 0.8;
  }
  
  #mask .center .left {
    left: 15px;
    text-align: left;
    padding-right: 10px;
    border-top-right-radius: 10px;
    border-bottom-right-radius: 10px;
  }
  
  #mask .center .right {
    right: 15px;
    text-align: right;
    padding-left: 10px;
    border-top-left-radius: 10px;
    border-bottom-left-radius: 10px;
  }
```



#### v-for 指令

**作用**： 根据数据生成列表结构（响应式）

- 数组经常和 *v-for* 结合使用
- 语法是 （*item,index) in 数组*
- item和 index 可以结合其他指令（v-bind,v-on等）一起使用
- 数组长度（数据）的更新会同步到页面上，是*响应式*的

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-for 指令</title>
</head>

<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">
        <input type="button" value="添加数据" @click="add">
        <input type="button" value="移除数据" @click="remove">
        <ul>
            <li v-for="item in arr">City: {{item}}</li> <!-- 这个item只是个变量名，可以修改的-->
            <li v-for="(it,index) in arr">序号： {{index}}</li>  <!-- index是数组里面的序号，从0开始-->
        </ul>
        <h2 v-for="item in vegetables" v-bind:title="item.name">    <!--对象数组的数据引用操作-->
            {{item.name}}
        </h2>
    </div>    
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{      // data 是数据对象
                arr:["西安","重庆","成都"],
                vegetables:[
                    {name:"肉夹馍"},
                    {name:"火锅"},
                    {name:"锅盔"}
                ]
            },
            methods:{
                add:function(){ //添加新的数组元素
                    this.vegetables.push({name:"快乐水才是真的快乐"});
                },
                remove:function(){  //移除最左边的数组元素
                    this.vegetables.shift();
                }
            }
         })
    </script>
</body>
</html>
```





#### v-on 指令补充

**作用**：传参自定义参数，事件修饰符

- 事件绑定的方法写成*函数调用*的形式，可以传入自定义参数（不需要数据类型，一个变量名即可）
- 定义方法时需要定义*形参*来接受传入的*实参*
- 事件的后面跟上 *.修饰符* 可以对事件进行限制
- *.enter* 可以限制触发的按键为回车
- 事件修饰符有多种，可以参考官方文档

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v- 指令</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">  
        <input type="button" value="点击我砍一刀" v-on:click="doIt('是兄弟就来砍我，一刀',9999)">  
       <input type="text" @keyup.enter="sayHi">  <!--keyup是键盘触发事件，点击Enter键的时候触发sayHi函数，不加.enter则点击任意键盘都会触发-->
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{
                food:"粗粗扒饭"
            },
            methods:{
                doIt:function(text,num){
                    alert(text+num);
                },
                sayHi:function(){
                    alert("老铁没毛病");
                }
               
            }
         })
    </script>
</body>
</html>
```





#### v-model 指令

**作用**：获取和设置表单元素的值（双向数据绑定，改表一边的数据，两边数据都会改变）

- 绑定的数据会和表单元素 *值* 相关联
- 绑定的数据——表单元素的值

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>v-model 指令</title>
</head>
<body>
    <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
    <div id="app">  
        <input type="button" value="修改message值" @click="setM">
        <input type="text" v-model="message" @keyup.enter="getM">   <!--用v-model指令将表单元素和message双向数据绑定-->
        <h2>{{message}}</h2>
    </div>
    
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
         var app =new Vue({
            el:"#app",  // el 是挂载点 ; # 是id选择器
            data:{
                message:"一giao我里giao"
            },
            methods:{
                getM:function(){
                    alert(this.message);
                },
                setM:function(){
                    this.message="狗皮giao药组合";
                }
            }
            
         })
    </script>
</body>
</html>
```





#### 小黑笔记本

 

| 功能 |                                                              |
| ---- | :----------------------------------------------------------- |
| 新增 | 1. 生成列表结构（v-for  数组）  2. 获取用户输入（v-model)    3. 回车，新增数据(v-on.emter 添加数据) |
| 删除 | 1. 点击删除指定内容（v-on splice  索引)                      |
| 统计 | 1. 统计信息个数（v-text  数组length)                         |
| 清空 | 1. 点击清除所有信息（v-on  清空数组)                         |
| 隐藏 | 1. 没有数据时，隐藏元素（v-show v-if  数组非空)              |

- 列表结构可以通过*v-for*指令结合数据生成
- *v-on*结合事件修饰符可以对事件进行限制，比如*.enter*
- *v-on*在绑定事件时可以传递自定义参数
- 通过*v-model*可以快速的设置和获取表单元素的值
- *基于数据*的开发方式



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>小黑记事本</title>
    <meta http-equiv="content-type" content="text/html; charset=UTF-8" />
    <meta name="robots" content="noindex, nofollow" />
    <meta name="googlebot" content="noindex, nofollow" />
    <meta name="viewport" content="width=device-width, initial-scale=1" />
    <link rel="stylesheet" type="text/css" href="notebook.css" />
</head>
<body>
        <!-- 主体区域 -->
        <section id="todoapp">
            <!-- 输入框 -->
            <header class="header">
              <h1>小黑记事本</h1>
              <input autofocus="autofocus" autocomplete="off" placeholder="请输入任务" class="new-todo" v-model="addValue" @keyup.enter="add(addValue)"/>
            </header>
            <!-- 列表区域 -->
            <section class="main">
              <ul class="todo-list">
                <li class="todo" v-for="(item,index) in list">
                  <div class="view">
                    <span class="index">{{index+1}}.</span> <label>{{item}}</label>
                    <button class="destroy" @click="remove(index)"></button>
                  </div>
                </li>
              </ul>
            </section>
            <!-- 统计和清空 -->
            <footer class="footer">
              <span class="todo-count" v-if="list.length!=0"> <strong>{{list.length}}</strong> items left </span>
              <button class="clear-completed" @click="clear" v-show="list.length!=0">
                Clear
              </button>
            </footer>
          </section>
          <!-- 底部 -->
          <footer class="info">
            <p>
              <a href="http://www.itheima.com/"><img src="http://www.itheima.com/images/logo.png" alt=""/></a>
            </p>
          </footer>
          <!-- 开发环境版本，包含了有帮助的命令行警告 -->
          <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
          <script>
              var app = new Vue({
                  el:"#todoapp",
                  data:{
                      list:["吃饭","睡觉","学习"],
                      addValue:"打游戏"
                  },
                  methods:{
                    add:function(value){
                        this.list.push(value)
                    },
                    remove:function(index){
                        this.list.splice(index,1)
                    },
                    clear:function(){
                        this.list=[]
                    }
                  }
              })
          </script>
</body>
</html>

```

```css
html,
body {
  margin: 0;
  padding: 0;
}
body {
  background: #fff;
}
button {
  margin: 0;
  padding: 0;
  border: 0;
  background: none;
  font-size: 100%;
  vertical-align: baseline;
  font-family: inherit;
  font-weight: inherit;
  color: inherit;
  -webkit-appearance: none;
  appearance: none;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

body {
  font: 14px "Helvetica Neue", Helvetica, Arial, sans-serif;
  line-height: 1.4em;
  background: #f5f5f5;
  color: #4d4d4d;
  min-width: 230px;
  max-width: 550px;
  margin: 0 auto;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  font-weight: 300;
}

:focus {
  outline: 0;
}

.hidden {
  display: none;
}

#todoapp {
  background: #fff;
  margin: 180px 0 40px 0;
  position: relative;
  box-shadow: 0 2px 4px 0 rgba(0, 0, 0, 0.2), 0 25px 50px 0 rgba(0, 0, 0, 0.1);
}

#todoapp input::-webkit-input-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}

#todoapp input::-moz-placeholder {
  font-style: italic;
  font-weight: 300;
  color: #e6e6e6;
}

#todoapp input::input-placeholder {
  font-style: italic;
  font-weight: 300;
  color: gray;
}

#todoapp h1 {
  position: absolute;
  top: -160px;
  width: 100%;
  font-size: 60px;
  font-weight: 100;
  text-align: center;
  color: rgba(175, 47, 47, .8);
  -webkit-text-rendering: optimizeLegibility;
  -moz-text-rendering: optimizeLegibility;
  text-rendering: optimizeLegibility;
}

.new-todo,
.edit {
  position: relative;
  margin: 0;
  width: 100%;
  font-size: 24px;
  font-family: inherit;
  font-weight: inherit;
  line-height: 1.4em;
  border: 0;
  color: inherit;
  padding: 6px;
  border: 1px solid #999;
  box-shadow: inset 0 -1px 5px 0 rgba(0, 0, 0, 0.2);
  box-sizing: border-box;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

.new-todo {
  padding: 16px;
  border: none;
  background: rgba(0, 0, 0, 0.003);
  box-shadow: inset 0 -2px 1px rgba(0, 0, 0, 0.03);
}

.main {
  position: relative;
  z-index: 2;
  border-top: 1px solid #e6e6e6;
}

.toggle-all {
  width: 1px;
  height: 1px;
  border: none; /* Mobile Safari */
  opacity: 0;
  position: absolute;
  right: 100%;
  bottom: 100%;
}

.toggle-all + label {
  width: 60px;
  height: 34px;
  font-size: 0;
  position: absolute;
  top: -52px;
  left: -13px;
  -webkit-transform: rotate(90deg);
  transform: rotate(90deg);
}

.toggle-all + label:before {
  content: "❯";
  font-size: 22px;
  color: #e6e6e6;
  padding: 10px 27px 10px 27px;
}

.toggle-all:checked + label:before {
  color: #737373;
}

.todo-list {
  margin: 0;
  padding: 0;
  list-style: none;
  max-height: 420px;
  overflow: auto;
}

.todo-list li {
  position: relative;
  font-size: 24px;
  border-bottom: 1px solid #ededed;
  height: 60px;
  box-sizing: border-box;
}

.todo-list li:last-child {
  border-bottom: none;
}

.todo-list .view .index {
  position: absolute;
  color: gray;
  left: 10px;
  top: 20px;
  font-size: 16px;
}

.todo-list li .toggle {
  text-align: center;
  width: 40px;
  /* auto, since non-WebKit browsers doesn't support input styling */
  height: auto;
  position: absolute;
  top: 0;
  bottom: 0;
  margin: auto 0;
  border: none; /* Mobile Safari */
  -webkit-appearance: none;
  appearance: none;
}

.todo-list li .toggle {
  opacity: 0;
}

.todo-list li .toggle + label {
  /*
		Firefox requires `#` to be escaped - https://bugzilla.mozilla.org/show_bug.cgi?id=922433
		IE and Edge requires *everything* to be escaped to render, so we do that instead of just the `#` - https://developer.microsoft.com/en-us/microsoft-edge/platform/issues/7157459/
	*/
  background-image: url("data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23ededed%22%20stroke-width%3D%223%22/%3E%3C/svg%3E");
  background-repeat: no-repeat;
  background-position: center left;
}

.todo-list li .toggle:checked + label {
  background-image: url("data:image/svg+xml;utf8,%3Csvg%20xmlns%3D%22http%3A//www.w3.org/2000/svg%22%20width%3D%2240%22%20height%3D%2240%22%20viewBox%3D%22-10%20-18%20100%20135%22%3E%3Ccircle%20cx%3D%2250%22%20cy%3D%2250%22%20r%3D%2250%22%20fill%3D%22none%22%20stroke%3D%22%23bddad5%22%20stroke-width%3D%223%22/%3E%3Cpath%20fill%3D%22%235dc2af%22%20d%3D%22M72%2025L42%2071%2027%2056l-4%204%2020%2020%2034-52z%22/%3E%3C/svg%3E");
}

.todo-list li label {
  word-break: break-all;
  padding: 15px 15px 15px 60px;
  display: block;
  line-height: 1.2;
  transition: color 0.4s;
}

.todo-list li.completed label {
  color: #d9d9d9;
  text-decoration: line-through;
}

.todo-list li .destroy {
  display: none;
  position: absolute;
  top: 0;
  right: 10px;
  bottom: 0;
  width: 40px;
  height: 40px;
  margin: auto 0;
  font-size: 30px;
  color: #cc9a9a;
  margin-bottom: 11px;
  transition: color 0.2s ease-out;
}

.todo-list li .destroy:hover {
  color: #af5b5e;
}

.todo-list li .destroy:after {
  content: "×";
}

.todo-list li:hover .destroy {
  display: block;
}

.todo-list li .edit {
  display: none;
}

.todo-list li.editing:last-child {
  margin-bottom: -1px;
}

.footer {
  color: #777;
  padding: 10px 15px;
  height: 20px;
  text-align: center;
  border-top: 1px solid #e6e6e6;
}

.footer:before {
  content: "";
  position: absolute;
  right: 0;
  bottom: 0;
  left: 0;
  height: 50px;
  overflow: hidden;
  box-shadow: 0 1px 1px rgba(0, 0, 0, 0.2), 0 8px 0 -3px #f6f6f6,
    0 9px 1px -3px rgba(0, 0, 0, 0.2), 0 16px 0 -6px #f6f6f6,
    0 17px 2px -6px rgba(0, 0, 0, 0.2);
}

.todo-count {
  float: left;
  text-align: left;
}

.todo-count strong {
  font-weight: 300;
}

.filters {
  margin: 0;
  padding: 0;
  list-style: none;
  position: absolute;
  right: 0;
  left: 0;
}

.filters li {
  display: inline;
}

.filters li a {
  color: inherit;
  margin: 3px;
  padding: 3px 7px;
  text-decoration: none;
  border: 1px solid transparent;
  border-radius: 3px;
}

.filters li a:hover {
  border-color: rgba(175, 47, 47, 0.1);
}

.filters li a.selected {
  border-color: rgba(175, 47, 47, 0.2);
}

.clear-completed,
html .clear-completed:active {
  float: right;
  position: relative;
  line-height: 20px;
  text-decoration: none;
  cursor: pointer;
}

.clear-completed:hover {
  text-decoration: underline;
}

.info {
  margin: 50px auto 0;
  color: #bfbfbf;
  font-size: 15px;
  text-shadow: 0 1px 0 rgba(255, 255, 255, 0.5);
  text-align: center;
}

.info p {
  line-height: 1;
}

.info a {
  color: inherit;
  text-decoration: none;
  font-weight: 400;
}

.info a:hover {
  text-decoration: underline;
}

/*
	Hack to remove background from Mobile Safari.
	Can't use it globally since it destroys checkboxes in Firefox
*/
@media screen and (-webkit-min-device-pixel-ratio: 0) {
  .toggle-all,
  .todo-list li .toggle {
    background: none;
  }

  .todo-list li .toggle {
    height: 40px;
  }
}

@media (max-width: 430px) {
  .footer {
    height: 50px;
  }

  .filters {
    bottom: 10px;
  }
}
```





### 三、网络应用

Vue结合网络数据开发应用

axios 网络请求库          axios+Vue

导入链接：<script src="https://unpkg.com/axios/dist/axios.min.js"></script>

[axios官网](了解axios更多用法请上：https://github.com/axios/axios)





#### axios基础

功能强大的**网络请求库**

- *axios* 必须先导入才可以使用   
- 使用*get*或*post*方法即可发送对应的请求
- *then*方法中的回调函数会在请求成功或失败的时候触发
- 通过回调函数的形参可以获取响应内容，或错误信息

```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <input type="button" value="axios:get请求" class="get">
    <input type="button" value="axios:post请求" class="post">
    
    <!-- 导入axios -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script>
        /*
            接口1:随机笑话
            请求地址:https://autumnfish.cn/api/joke/list
            请求方法:get
            请求参数:num(笑话条数,数字)
            响应内容:随机笑话
        */
        document.querySelector(".get").onclick = function () {
            axios.get("https://autumnfish.cn/api/joke/list?num=4")
            // axios.get("https://autumnfish.cn/api/joke/qewqeq?num=6")
            .then(function (response) {
                console.log(response);
              },function(err){
                  console.log(err);
              })
        }
        /*
             接口2:用户注册
             请求地址:https://autumnfish.cn/api/user/reg
             请求方法:post
             请求参数:username(用户名,字符串)
             响应内容:注册成功或失败
         */
         document.querySelector(".post").onclick = function(){
            axios.post("https://autumnfish.cn/api/user/reg",{username:"asgdyufgq"})
            .then(function(response){
                console.log(response);
            },function(err){
                console.log(err);
            })
        }
    </script>
</body>
</html>

```





#### axios+Vue

axios如何结合Vue开发网络应用



- axios回调函数中的*this已经改变*，无法访问到data中的数据，
- 所以先把this保存起来，回调函数使用*保存的this*（定义一个that 来访问data）
- 网络应用和本地应用最大的区别就是改变了*数据来源*



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>axios+Vue</title>
</head>
<body>
   
     <!-- 实用简洁的*模板语法*把数据渲染到页面上 -->
     <div id="app">
        <input type="button" value="获取笑话" @click="getjoke">
        <p>{{joke}}</p>
    </div>    
    
    <!-- 导入axios -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
   
    <!-- 导入Vue 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    
    <!-- 创建Vue实例对象，设置el和data属性 -->
    <script>
        /*
            接口1:随机笑话
            请求地址:https://autumnfish.cn/api/joke
            请求方法:get
            请求参数:num(笑话条数,数字)
            响应内容:随机笑话
        */
        var app = new Vue({
            el:"#app",
            data:{
                joke:"一个笑话"
            },
            methods:{
                getjoke:function(){
                    var that = this;    //axios回调函数中的this已经改变，无法访问到data中的数据，所以定义一个that 来访问data
                    axios.get("https://autumnfish.cn/api/joke").then(
                        function(response){
                            // console.log(response);
                            // console.log(response.data);
                            that.joke = response.data;
                        },
                        function(err){
                            console.log(err);
                        }
                    )
                }
            }
        })
        
    </script>
</body>
</html>
```





#### 天知道(天气预报应用)

回车查询  

1. 按下回车（v-on  .enter)
2. 查询数据（axios  api接口   v-model)
3. 渲染数据（v-for 数组 that )

点击查询

1. 点击城市（v-on 自定义参数）
2. 查询数据（this.()方法）
3. 渲染数据

- 应用的逻辑代码建议和页面*分离*，使用*单独的 js*文件编写
- 服务器返回的数据比较复杂时，获取的时候注意*层级* 结构
- 自定义的参数可以让代码的*复用性*更高
- methods中定义的方法内部，可以通过*this关键字*点出其他方法



```html
天知道.html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>天知道</title>
    <link rel="stylesheet" href="reset.css" />
    <link rel="stylesheet" href="index.css" />
  </head>

  <body>
    <div class="wrap" id="app">
      <div class="search_form">
        <div class="logo"><img src="//i0.hdslb.com/bfs/face/eb58f347d560732b545cbee17557429fb9a43f9f.jpg_64x64.jpg" alt="logo" /></div>
        <div class="form_group">
          <input type="text" class="input_txt" placeholder="请输入查询的天气"
            v-model="city" @keyup.enter="getWeather"/>
          <button class="input_sub">
            搜 索
          </button>
        </div>
        <div class="hotkey">
          <a href="javascript:;" @click="queryWeather('北京')">北京</a>
          <a href="javascript:;" @click="queryWeather('上海')">上海</a>
          <a href="javascript:;" @click="queryWeather('广州')">广州</a>
          <a href="javascript:;" @click="queryWeather('深圳')">深圳</a>
        </div>
      </div>
      <ul class="weather_list">
        <li v-for="item in weatherList">
          <div class="info_type"><span class="iconfont">{{item.type}}</span></div>
          <div class="info_temp">
            <b>{{item.low}}</b>
            ~
            <b>{{item.high}}</b>
          </div>
          <div class="info_date"><span>{{item.date}}</span></div>
        </li>
      </ul>
    </div>
<body>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- 官网提供的 axios 在线地址 -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <!-- 自己的js -->
    <script src="weather.js"></script>
</body>
</html>

```

```css
index.css
body{
    font-family:'Microsoft YaHei';   
}
.wrap{
    position: fixed;
    left:0;
    top:0;
    width:100%;
    height:100%;
    /* background: radial-gradient(#f3fbfe, #e4f5fd, #8fd5f4); */
    /* background:#8fd5f4; */
    /* background: linear-gradient(#6bc6ee, #fff); */
    background:#fff;

}
.search_form{
    width:640px;
    margin:100px auto 0;
}
.logo img{
    display:block;
    margin:0 auto;
}
.form_group{
    width:640px;
    height:40px;
    margin-top:45px;
}
.input_txt{
   width:538px;
   height:38px;
   padding:0px;
   float:left;
   border:1px solid #41a1cb;
   outline:none;
   text-indent:10px;
}

.input_sub{
    width:100px;
    height:40px;
    border:0px;
    float: left;
    background-color: #41a1cb;
    color:#fff;
    font-size:16px;
    outline:none;
    cursor: pointer;
    position: relative;
}
.input_sub.loading::before{
    content:'';
    position: absolute;
    left: 0;
    top: 0;
    width: 100%;
    height: 100%;
    background: url('https://i0.hdslb.com/bfs/archive/ed8d99a0a1ad657cf4dce599327517876ea06034.jpg@152w_152h_100Q_1c.webp');
}

.hotkey{
    margin:3px 0 0 2px;
}

.hotkey a{
    font-size:14px;
    color:#666;
    padding-right:15px;
}
.weather_list{
    height:200px;
    text-align:center;
    margin-top:50px;
    font-size:0px;
}
.weather_list li{
    display:inline-block;
    width:140px;
    height:200px;
    padding:0 10px;
    overflow: hidden;
    position: relative;
    background:url('https://s1.hdslb.com/bfs/static/jinkela/space/asserts/icon-auth.png') right center no-repeat;
    background-size: 1px 130px;
}

.weather_list li:last-child{
    background:none;
}

/* .weather_list .col02{
    background-color: rgba(65, 165, 158, 0.8);
}
.weather_list .col03{
    background-color: rgba(94, 194, 237, 0.8);
}
.weather_list .col04{
    background-color: rgba(69, 137, 176, 0.8);
}
.weather_list .col05{
    background-color: rgba(118, 113, 223, 0.8);
} */


.info_date{
    width:100%;
    height:40px;
    line-height:40px;
    color:#999;
    font-size:14px;
    left:0px;    
    bottom:0px;    
    margin-top: 15px;
}
.info_date b{
    float: left;
    margin-left:15px;
}

.info_type span{
    color:#fda252;
    font-size:30px;
    line-height:80px;
}
.info_temp{
    font-size:14px;  
    color:#fda252;
}
.info_temp b{
    font-size:13px;
}
.tem .iconfont {
    font-size: 50px;
  }
```

```css
reset.css
body,ul,h1,h2,h3,h4,h5,h6{
    margin: 0;
    padding: 0;
}
h1,h2,h3,h4,h5,h6{
    font-size:100%;
    font-weight:normal;
}
a{
    text-decoration:none;
}
ul{
    list-style:none;
}
img{
    border:0px;
}

/* 清除浮动，解决margin-top塌陷 */
.clearfix:before,.clearfix:after{
    content:'';
    display:table;    
}
.clearfix:after{
    clear:both;
}
.clearfix{
    zoom:1;
}

.fl{
    float:left;
}
.fr{
    float:right;
}
```

```js
weather.js
/*
  请求地址:http://wthrcdn.etouch.cn/weather_mini
  请求方法:get
  请求参数:city(城市名)
  响应内容:天气信息
  1. 点击回车
  2. 查询数据
  3. 渲染数据
*/

var app = new Vue({
    el:"#app",
    data:{
        city:"",
        weatherList:[]
    },
    methods:{
        getWeather:function(){
            var that = this;
            axios.get("http://wthrcdn.etouch.cn/weather_mini?city="+this.city)
            .then(function(response){
                that.weatherList = response.data.data.forecast;
            },function(err){})
        },
        queryWeather:function(city){
            this.city = city;
            this.getWeather();
        }
    }
})
```





### 四、综合应用

悦听播放器

1. 歌曲搜索
   1. 按下回车（v-on .enter)
   2. 查询数据（axios  接口 v-model)
   3. 渲染数据（v-for 数组 that)
2. 歌曲播放
3. 歌曲封面
4. 歌曲评论
5. 播放动画
6. mv播放



```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>悦听player</title>
    <link rel="stylesheet" href="./css/index.css">
  </head>
  
  <body>
    <div class="wrap">
      <!-- 播放器主体区域 -->
      <div class="play_wrap" id="player">
        <div class="search_bar">
          <img src="images/player_title.png" alt="" />
          <!-- 搜索歌曲 -->
          <input type="text" autocomplete="off" v-model="musicName" @keyup.enter="searchMusic" />
        </div>
        <div class="center_con">
          <!-- 搜索歌曲列表 -->
          <div class='song_wrapper'>
            <ul class="song_list">
             <li v-for="item in musicList">
                 <a href="javascript:;" @click="playMusic(item.id)"></a> 
                 <b>{{item.name}}</b> 
                 <span><i @click="getMV(item.mvid)" v-if="item.mvid!=0"></i></span>
             </li>
            </ul>
            <img src="images/line.png" class="switch_btn" alt="">
          </div>
          <!-- 歌曲信息容器 -->
          <div class="player_con" :class="{playing:isPlaying}">
            <img src="images/player_bar.png" class="play_bar" />
            <!-- 黑胶碟片 -->
            <img src="images/disc.png" class="disc autoRotate" />
            <img :src="musicCover" class="cover autoRotate" />
          </div>
          <!-- 评论容器 -->
          <div class="comment_wrapper">
            <h5 class='title'>热门留言</h5>
            <div class='comment_list'>
              <dl v-for="item in hotCommentList">
                <dt><img :src="item.user.avatarUrl" alt=""></dt>
                <dd class="name">{{item.user.nickname}}</dd>
                <dd class="detail">
                  {{item.content}}
                </dd>
              </dl>
            </div>
            <img src="images/line.png" class="right_line">
          </div>
        </div>
        <div class="audio_con">
          <audio ref='audio' @play="play" @pause="pause" :src="musicUrl" controls autoplay loop class="myaudio"></audio>
        </div>
        <div class="video_con"  style="display: none;" v-show="isShow">
          <video  controls="controls" :src="mvUrl"></video>
          <div class="mask" @click="hide"></div>
        </div>
      </div>
    </div>
    <!-- 开发环境版本，包含了有帮助的命令行警告 -->
    <script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
    <!-- 官网提供的 axios 在线地址 -->
    <script src="https://unpkg.com/axios/dist/axios.min.js"></script>
    <script src="./js/main.js"></script>
</body>
</html>
```

```js
main.js
/*
  1:歌曲搜索接口
    请求地址:https://autumnfish.cn/search
    请求方法:get
    请求参数:keywords(查询关键字)
    响应内容:歌曲搜索结果
  2:歌曲url获取接口
    请求地址:https://autumnfish.cn/song/url
    请求方法:get
    请求参数:id(歌曲id)
    响应内容:歌曲url地址
  3.歌曲详情获取
    请求地址:https://autumnfish.cn/song/detail
    请求方法:get
    请求参数:ids(歌曲id)
    响应内容:歌曲详情(包括封面信息)
  4.热门评论获取
    请求地址:https://autumnfish.cn/comment/hot?type=0
    请求方法:get
    请求参数:id(歌曲id,地址中的type固定为0)
    响应内容:歌曲的热门评论
  5.mv地址获取
    请求地址:https://autumnfish.cn/mv/url
    请求方法:get
    请求参数:id(mvid,为0表示没有mv)
    响应内容:mv的地址
*/

var app = new Vue({
    el:"#player",
    data:{
        //歌曲名称
        musicName:"",
        //歌曲列表
        musicList:[],
        //歌曲地址
        musicUrl:"",
        //歌曲封面
        musicCover:"",
        //热门评论
        hotCommentList:[],
        //歌曲MV
        mvUrl:"",
        //封面状态
        isPlaying:false,
        // 遮罩层状态
        isShow:false
    },
    methods:{
        //搜索歌曲
        searchMusic:function(){
            var that = this;
            axios.get("https://autumnfish.cn/search?keywords="+this.musicName)
            .then(function(response){
                //console.log(response.data.result.songs)
                that.musicList = response.data.result.songs;
            },function(err){})
        },
        //播放歌曲
        playMusic:function(musicId){
            var that = this;
            axios.get("https://autumnfish.cn/song/url?id="+musicId)
            .then(function(response){
                //console.log(response.data.data[0].url)
                that.musicUrl = response.data.data[0].url;
            },function(err){})
            //歌曲封面
            axios.get("https://autumnfish.cn/song/detail?ids="+musicId)
            .then(function(response){
                //console.log(response.data.songs[0].al.picUrl)
                that.musicCover = response.data.songs[0].al.picUrl;
            },function(err){})
            //热门评论
            axios.get("https://autumnfish.cn/comment/hot?type=0&id="+musicId)
            .then(function(response){
                //console.log(response.data.hotComments)
                that.hotCommentList = response.data.hotComments;
            },function(err){})
        },
        // 歌曲播放
        play: function() {
            // console.log("play");
            this.isPlaying = true;
        },
        // 歌曲暂停
        pause: function() {
            // console.log("pause");
            this.isPlaying = false;
        },
        // 播放mv
        getMV:function(mvid) {
            var that = this;
            axios.get("https://autumnfish.cn/mv/url?id="+mvid).then(
            function(response) {
                console.log(response.data.data.url);
                that.isShow = true;
                that.mvUrl = response.data.data.url;
            },
                function(err) {}
            );
        },
        hide:function() {
            this.isShow = false;
        }
    }
})
```

```css
index.css
body,
ul,
dl,
dd {
  margin: 0px;
  padding: 0px;
}

.wrap {
  position: fixed;
  left: 0;
  top: 0;
  width: 100%;
  height: 100%;
  background: url("../images/bg.jpg") no-repeat;
  background-size: 100% 100%;
}

.play_wrap {
  width: 800px;
  height: 544px;
  position: fixed;
  left: 50%;
  top: 50%;
  margin-left: -400px;
  margin-top: -272px;
  /* background-color: #f9f9f9; */
}

.search_bar {
  height: 60px;
  background-color: #1eacda;
  border-top-left-radius: 4px;
  border-top-right-radius: 4px;
  display: flex;
  align-items: center;
  justify-content: space-between;
  position: relative;
  z-index: 11;
}

.search_bar img {
  margin-left: 23px;
}

.search_bar input {
  margin-right: 23px;
  width: 296px;
  height: 34px;
  border-radius: 17px;
  border: 0px;
  background: url("../images/zoom.png") 265px center no-repeat
    rgba(255, 255, 255, 0.45);
  text-indent: 15px;
  outline: none;
}

.center_con {
  height: 435px;
  background-color: rgba(255, 255, 255, 0.5);
  display: flex;
  position: relative;
}

.song_wrapper {
  width: 200px;
  height: 435px;
  box-sizing: border-box;
  padding: 10px;
  list-style: none;
  position: absolute;
  left: 0px;
  top: 0px;
  z-index: 1;
}

.song_stretch {
  width: 600px;
}

.song_list {
  width: 100%;
  overflow-y: auto;
  overflow-x: hidden;
  height: 100%;
}
.song_list::-webkit-scrollbar {
  display: none;
}

.song_list li {
  font-size: 12px;
  color: #333;
  height: 40px;
  display: flex;
  flex-wrap: wrap;
  align-items: center;
  width: 580px;
  padding-left: 10px;
}

.song_list li:nth-child(odd) {
  background-color: rgba(240, 240, 240, 0.3);
}

.song_list li a {
  display: block;
  width: 17px;
  height: 17px;
  background-image: url("../images/play.png");
  background-size: 100%;
  margin-right: 5px;
  box-sizing: border-box;
}

.song_list li b {
  font-weight: normal;
  width: 122px;
  overflow: hidden;
  text-overflow: ellipsis;
  white-space: nowrap;
}

.song_stretch .song_list li b {
  width: 200px;
}

.song_stretch .song_list li em {
  width: 150px;
}

.song_list li span {
  width: 23px;
  height: 17px;
  margin-right: 50px;
}
.song_list li span i {
  display: block;
  width: 100%;
  height: 100%;
  cursor: pointer;
  background: url("../images/table.png") left -48px no-repeat;
}

.song_list li em,
.song_list li i {
  font-style: normal;
  width: 100px;
}

.player_con {
  width: 400px;
  height: 435px;
  position: absolute;
  left: 200px;
  top: 0px;
}

.player_con2 {
  width: 400px;
  height: 435px;
  position: absolute;
  left: 200px;
  top: 0px;
}

.player_con2 video {
  position: absolute;
  left: 20px;
  top: 30px;
  width: 355px;
  height: 265px;
}

.disc {
  position: absolute;
  left: 73px;
  top: 60px;
  z-index: 9;
}
.cover {
  position: absolute;
  left: 125px;
  top: 112px;
  width: 150px;
  height: 150px;
  border-radius: 75px;
  z-index: 8;
}
.comment_wrapper {
  width: 180px;
  height: 435px;
  list-style: none;
  position: absolute;
  left: 600px;
  top: 0px;
  padding: 25px 10px;
}
.comment_wrapper .title {
  position: absolute;
  top: 0;
  margin-top: 10px;
}
.comment_wrapper .comment_list {
  overflow: auto;
  height: 410px;
}
.comment_wrapper .comment_list::-webkit-scrollbar {
  display: none;
}
.comment_wrapper dl {
  padding-top: 10px;
  padding-left: 55px;
  position: relative;
  margin-bottom: 20px;
}

.comment_wrapper dt {
  position: absolute;
  left: 4px;
  top: 10px;
}

.comment_wrapper dt img {
  width: 40px;
  height: 40px;
  border-radius: 20px;
}

.comment_wrapper dd {
  font-size: 12px;
}

.comment_wrapper .name {
  font-weight: bold;
  color: #333;
  padding-top: 5px;
}

.comment_wrapper .detail {
  color: #666;
  margin-top: 5px;
  line-height: 18px;
}
.audio_con {
  height: 50px;
  background-color: #f1f3f4;
  border-bottom-left-radius: 4px;
  border-bottom-right-radius: 4px;
}
.myaudio {
  width: 800px;
  height: 40px;
  margin-top: 5px;
  outline: none;
  background-color: #f1f3f4;
}
/* 旋转的动画 */
@keyframes Rotate {
  from {
    transform: rotateZ(0);
  }
  to {
    transform: rotateZ(360deg);
  }
}
/* 旋转的类名 */
.autoRotate {
  animation-name: Rotate;
  animation-iteration-count: infinite;
  animation-play-state: paused;
  animation-timing-function: linear;
  animation-duration: 5s;
}
/* 是否正在播放 */
.player_con.playing .disc,
.player_con.playing .cover {
  animation-play-state: running;
}

.play_bar {
  position: absolute;
  left: 200px;
  top: -10px;
  z-index: 10;
  transform: rotate(-25deg);
  transform-origin: 12px 12px;
  transition: 1s;
}
/* 播放杆 转回去 */
.player_con.playing .play_bar {
  transform: rotate(0);
}
/* 搜索历史列表 */
.search_history {
  position: absolute;
  width: 296px;
  overflow: hidden;
  background-color: rgba(255, 255, 255, 0.3);
  list-style: none;
  right: 23px;
  top: 50px;
  box-sizing: border-box;
  padding: 10px 20px;
  border-radius: 17px;
}
.search_history li {
  line-height: 24px;
  font-size: 12px;
  cursor: pointer;
}
.switch_btn {
  position: absolute;
  right: 0;
  top: 0;
  cursor: pointer;
}
.right_line {
  position: absolute;
  left: 0;
  top: 0;
}
.video_con video {
  position: fixed;
  width: 800px;
  height: 546px;
  left: 50%;
  top: 50%;
  margin-top: -273px;
  transform: translateX(-50%);
  z-index: 990;
}
.video_con .mask {
  position: fixed;
  width: 100%;
  height: 100%;
  left: 0;
  top: 0;
  z-index: 980;
  background-color: rgba(0, 0, 0, 0.8);
}
.video_con .shutoff {
  position: fixed;
  width: 40px;
  height: 40px;
  background: url("../images/shutoff.png") no-repeat;
  left: 50%;
  margin-left: 400px;
  margin-top: -273px;
  top: 50%;
  z-index: 995;
}


```

