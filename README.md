# vue_learn
## vscode插件推荐
1. jshint: js代码规范检查。
2. Beautify：一键美化代码的插件。
3. Vetur：.vue文件识别插件。
4. Javascript(ES6) code snippets：ES6语法提示。
5、 Auto Rename Tag：自动重命名标签。标签都是成对出现的，开始标签修改了，结束标签也会跟着修改。
6. Auto Close Tag：自动闭合标签。针对一些非标准的标签，这个插件还是很有用的。
7. vue helper：一些Vue代码的快捷代码。
8. vscode-icons：可选。提供了很多类型的文件夹icon，不同类型的文件夹使用不同的icon，会让文件查找更直观。
9. open in browser：可选。右键可以选择在默认浏览器中打开当前网页。

## vue介绍
Vue(读音/vjuː/，类似于view) 是一套用于构建前后端分离的框架。刚开始是由国内优秀选手尤雨溪开发出来的，目前是全球“最”流行的前端框架。

#### vue安装和使用
vue的安装大体上分成三种方式，第一种是通过script标签引用的，第二种是通过npm(node package manager)来安装，第三种是通过vue-cli命令行来安装。
```html
# 开发环境
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
# 或者是指定版本号
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.js"></script>
# 或者是下载代码保存到本地
<script src="lib/vue.js"></script>


# 生产环境，使用压缩后的文件
<script src="https://cdn.jsdelivr.net/npm/vue@2.6.10/dist/vue.min.js"></script>
```

#### 基本使用
1. 要使用Vue，首先需要创建一个Vue对象，并且在这个对象中传递el参数，el参数全称是element，用来找到一个给vue渲染的根元素。并且我们可以传递一个data参数，data中的所有值都可以直接在根元素下使用{{}}来使用。
2. 其中data中的数据，只能在vue的根元素下使用，在其他地方是不能被vue识别和渲染的
3. 另外也可以在vue对象中添加methods，这个属性中专门用来存储自己的函数。methods中的函数也可以在模板中使用，并且在methods中的函数来访问data中的值，只需要通过this.属性名就可以访问到了，不需要额外加this.data.属性名来访问。

下方代码参考01demo.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>my_demo</title>
</head>
<body>
    <div id="app">
        <!-- vue对象传递的参数需要{{}}包裹 -->
        <p>{{username}}</p>
        <p>{{greet()}}</p>
    </div>
</body>
</html>
<!-- 无需下载，通过下方链接使用vue -->
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    // 创建vue对象，传递el参数，data可以用来传递参数
    let vm = new Vue({
        // #就是id，指向body中id="app"
        el: "#app",
        data: {
            'username': '宝贝猪猪'
        },
        // vue对象中通过methods存储函数，函数访问data中的变量需要通过this
        // this表示当前对象
        methods: {
            greet: function(){
                return "晚上好！" + this.username
            }
        }
    });
</script>
```

## vue模板语法
1. 在html中通过{{}}（双大括号）中可以把Vue对象中的数据插入到网页中。并且只要Vue对象上对应的值发生改变了，那么html中双大括号中的值也会立马改变。
2. 有时候我们的Vue对象中，或者是后台返回给我们一个段原生的html代码，我们需要渲染出来，那么如果直接通过{{}}渲染，会把这个html代码当做字符串。这时候我们就可以通过v-html指令来实现。
3. 如果我们想要在html元素的属性上绑定我们Vue对象中的变量，那么需要通过v-bind来实现。

下方代码参考02vue_template_learn.html
```html
<body>
    <div id='app'>
        <h1>{{username}}</h1>
        <!-- button标签点击后有惊喜，点击会调用vue对象中methods里的change方法 -->
        <button @click='change'>suprise</button>
        <!-- v-html可以渲染原生的html代码 -->
        <div v-html='code'></div>
        <!-- ":"是v-bind:的简写，如果想在html中绑定vue对象中的变量，通过v-bind来实现
        即绑定对象的对象改变，显示值也会改变 -->
        <img :src="imagesrc" alt="">
    </div>
</body>
</html>

<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script>
    new Vue({
        el: '#app',
        data: {
            'username': '黄猪猪',
            'code': "<a href='https://www.baidu.com/'>百度一下，你就知道！</a>",
            'imagesrc': 'https://www.baidu.com/img/bd_logo1.png?qua=high&where=super'
        },
        methods: {
            change: function(){
                this.username = '我好稀饭你'
            }
        }
    })
</script>
```

4. 绑定属性 & 绑定style
    - 通过数组/对象的方式
5. 使用javascript表达式，三元表达式
6. 条件判断
7. 循环
    - 循环数组/对象
8. v-show & v-if

v-if是“真正”的条件渲染，因为它会确保在切换过程中条件块内的事件监听器和子组件适当地被销毁和重建。 v-if也是惰性的：如果在初始渲染时条件为假，则什么也不做——直到条件第一次变为真时，才会开始渲染条件块。 相比之下，v-show就简单得多——不管初始条件是什么，元素总是会被渲染，并且只是简单地基于CSS进行切换。 一般来说， v-if有更高的切换开销，而v-show有更高的初始渲染开销。因此，如果需要非常频繁地切换，则使用v-show较好；如果在运行时条件很少改变，则使用v-if较好。

下方代码参考03bind_attr.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>vue02</title>
    <!-- css 样式 -->
    <style>
        .title{
            font-size: 40px;
            color: red;
        }
        .main_title{
            font-weight: 80;
        }
    </style>
</head>
<body>
    <p class="title">中国，加油！</p>
    <div id='app'>
        <!-- 属性绑定 -->
        <!-- 通过数组的方法绑定css中的样式，效果等同于“中国，加油！” -->
        <p v-bind:class='[class1, class2]'>china fighting!!!</p>
        <!-- 通过对象的方法绑定css中的样式,效果同上 -->
        <p v-bind:class="{title:class3, main_title:class4}">china fighting!!!</p>
        
        <!-- 绑定style -->
        <!-- 通过对象的方法,读取对应样式的值 -->
        <p v-bind:style="{'backgroundColor': background}">hi</p>
        <!-- 通过数组的方法，读取对应样式的值，若有多组可以使用'[pcl1, pcl2]' -->
        <P v-bind:style='pcl'>嘟嘟嘟~</P>

        <!-- 使用JavaScript表达式 -->
        <!-- {color:color?"red":"blue"}是一个三元表达式（三目），如果vue对象有定义color
        就显示红色，没有显示蓝色 -->
        <!-- username.split(" ").reverse().join(" ")，是javascript表达式，split是去除指定内容
        reverse()是翻转，join是拼接指定内容。该语句的效果是将world hello 变成 hello world -->
        <p :style='{color:color?"red":"blue"}'>{{username.split(" ").reverse().join(" ")}}</p>
        
        <!-- 条件判断 -->
        <p v-if="weather == 'sun' " :style='pcl'>出去耍</p>
        <p v-else-if="weather == 'rain' ">在家耍</p>
        <p v-else>恰火锅</p>
    </div>

    <!-- 切换不同的登录方式，指定key属性可以在每次切换后保持输入框空白 -->
    <div id='login'>
        <template v-if="logintype == 'username' ">
            <label>用户名</label>
            <input type="text" placeholder='用户名' key='username'>
        </template>
        <template v-else-if="logintype == 'email'">
            <label>邮箱</label>
            <input type="text" placeholder='邮箱' key='email'>
        </template>
        <button v-on:click="checkout">切换</button>
    </div>

    <!-- 循环 -->
    <div class='hi'>
        <table>
            <tr>
                <th>序号</th>
                <th>书名</th>
                <th>作者</th>
            </tr>
            
            <!-- 循环数组 -->
            <tr v-for="(book,index) in books">
                <td>{{index+1}}</td>
                <td>{{book.name}}</td>
                <td>{{book.auth}}</td>
            </tr>
        </table>

        <!-- 循环对象 -->
        <div v-for='(value, key) in person'>
            {{key}}:{{value}}
        </div>
    </div>


</body>
</html>

<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script>
    new Vue({
        el: '#app',
        data: {
            class1: 'title',
            class2: 'main_title',
            class3: true,
            class4: true,
            background: 'red',
            pcl: {
                backgroundColor: 'pink',
                // 字符串中有 - 需要用引号包裹，或者改成驼峰命名
                'font-size': '60px'
            },
            username: 'world hello',
            color: false,
            weather: 'sun'
        }
    });
    new Vue({
        el: '#login',
        data: {
            logintype: 'username'
        },
        methods: {
            checkout: function(){
                this.logintype = this.logintype=='username'?'email':'username';
            }
        }
    });
    new Vue({
        el: '.hi',
        data: {
            books: [
                {
                    name: 'python',
                    auth: '龟叔'
                },
                {
                    name: '凡心春水',
                    auth: '冰心'
                },
                {
                    name: '追风筝的人',
                    auth: '啦啦啦'
                }
            ],
            person: {
                username: 'shell',
                age: '16'
            }
        }
    })
</script>
```