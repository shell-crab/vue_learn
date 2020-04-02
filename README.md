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

1. 绑定属性 & 绑定style
    - 通过数组/对象的方式
2. 使用javascript表达式，三元表达式
3. 条件判断
4. 循环
    - 循环数组/对象
5. 循环出来的元素，如果没有使用key元素来唯一标识，如果后期的数据发生了更改，默认是会重用的，并且元素的顺序不会跟着数据的顺序更改而更改
6. v-show & v-if

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

1. sort()函数
    - sort()  方法用于对数组的元素进行排序，并返回数组。默认排序顺序是根据字符串UniCode码。
2. v-on/@ 事件绑定
3. 触发视图更新
4. 动态添加属性
5. 传入event参数

下方代码参考04templates01.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id='app'>
        <h1>sort()函数的使用</h1>
        <div v-for='l in language' :key="l">
            <label for="">{{l}}</label>
            <input type="text" :placeholder="l">
        </div>
        <!-- <p>@click是v-on:click的简写方式，当点击该按钮时调用change方法</p> -->
        <button @click='change'>位置调换</button>


        <h1 style="background-color: red;">触发视图更新</h1>
        <div v-for="l in language">
            <p>{{l}}</p>
        </div>
        <button @click='usePush'>push</button>
        <button @click='updata'>change</button>
        <button @click='usePop'>pop</button>
        <button @click='useShift'>shift</button>


        <h1 style="background-color: pink;">动态添加属性</h1>
        <div v-for='i in person'>
            <p>{{i}}</p>
        </div>
        <!-- 可以通过这种方式访问username变量 -->
        <p>{{person.username}}</p>
        <button @click='add'>add</button>


        <h1 style="background-color: salmon;">传入event参数</h1>
        <div>
            <p>{{count}}</p>
            <!-- 绑定事件可直接放到v-on/@ 后面 -->
            <button @click="count += 1">加1</button>
            <!-- 或是也是一个函数，并且可以传递参数 -->
            <button v-on:click="sub(2, $event)" value='giao' name='ha'>减2</button>
        </div>
    </div>
</body>
</html>

<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script>
    new Vue({
        el: '#app',
        data: {
            language: ['python', 'java', 'C', 'PHP'],
            person: {
                username: 'shell'
            },
            count: 0
        },
        methods: {
            change: function(){
                // 伪随机
                // sort让language中的字符串两两比较，return会返回正数、负数或0
                // 返回负数时，a、b按照升序排列
                // 返回正数时，a、b按照降序排列
                // 返回0， 不变
                this.language.sort(function (a, b){
                    return 5 - Math.random()*10
                })
            },

            // 触发视图更新
            usePush: function(){
                // 向尾部添加元素
                this.language.push("够浪")
            },

            usePop: function(){
                // 删除最后一个元素
                this.language.pop()
            },

            useShift: function(){
                // 删除数组第一个元素，unshift向数组开头位置添加一个元素
                this.language.shift()
            },

            updata: function(){
                // 替换---从下标0开始，将长度为2的数组元素替换为shell
                // this.language.splice(0,2,'shell', 'crab')

                // 删除---从下标0开始，删除长度为2
                // this.language.splice(0,2)

                // 添加---在下标1的位置添加shell
                // this.language.splice(1,0,'shell')

                // 将数组元素进行翻转
                // this.language.reverse()

                // 改变数组元素使用set()方法或splice()方法
                Vue.set(this.language, 0, 'shell')
            },

            add: function(){
                Vue.set(this.person, 'age', 18)
            },

            // 上面传递了event参数，这里就需要接受，event可以获取原生的DOM事件
            sub: function(num, event){
                this.count -= num
                console.log(b.target.value)
                console.log(b.target.name)
            }
        }
    })
</script>
```
## 计算属性和监听器
1. 可能有的小伙伴会觉得这个计算属性跟之前的函数好像有点重复。实际上，计算属性更加智能，他是基于它们的响应式依赖进行缓存的。也就是说只要相关依赖没有发生改变，那么这个计算属性的函数不会重新执行，而是直接返回之前的值。这个缓存功能让计算属性访问更加高效。
2. 计算属性默认只有get，不过在需要时你也可以提供一个set，但是提供了set就必须要提供get方法。示例代码如下：
3. 监听属性可以针对某个属性进行监听，只要这个属性的值发生改变了，那么就会执行相应的函数。

下方代码参考05计算属性&监听.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>computed&watch_learn</title>
</head>
<body>
    <div id='app'>
        <h1>计算属性</h1>
        <!-- v-model是双向绑定，在页面中改变length的值，代码中也会改变 -->
        <div>
            <label for="">长：</label>
            <input type="number" name="length" v-model:value="length">
        </div>
        <div>
            <label for="">宽：</label>
            <input type="number" name="weight" v-model:value="weight">
        </div>
        <div>
            <label for="">面积：</label>
            <input type="text" name="area" readonly v-bind:value="area">
        </div>


        <h1>计算属性的set</h1>
        <p>尝试输入广东、广州、天河 或是 在详细地址输入广东省广州市天河区</p>
        <div>
            <label for="">省：</label>
            <input type="text" name="province" v-model:value="province">
        </div>
        <div>
            <label for="">市：</label>
            <input type="text" name="city" v-model:value="city">
        </div>
        <div>
            <label for="">区：</label>
            <input type="text" name="district" v-model:value="district">
        </div>
        <div>
            <label for="">详细地址：</label>
            <input type="text" name="address" v-model:value='address'>
        </div>


        <h1>监听属性</h1>
        <div>
            <label for="">搜索</label>
            <input type="text" name="keyword" v-model="keyword">
        </div>
        <div>
            <p>结果:{{answer}}</p>
        </div>
    </div>
</body>
</html>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script>
    new Vue({
        el: '#app',
        data: {
            length: 0,
            weight: 0,
            province: '',
            city: '',
            district: '',
            answer: "",
            keyword: ""
        },
        computed:{
            area: function(){
                return this.length * this.weight
            },
            address: {
                get: function(){
                    var result = "";
                    if(this.province){
                        result = this.province + '省';    
                    }
                    if(this.city){
                        result += this.city + '市';
                    }
                    if(this.district){
                        result += this.district + '区';
                    }
                    // console.log(result)
                    return result;
                },
                set: function(addr){
                    // 广东省广州市天河区
                    var result = addr.split(/省|市|区/)
                    // console.log(result)
                    if(result && result.length>0){
                        this.province = result[0]
                    }
                    if(result && result.length>1){
                        this.city = result[1]
                    }
                    if(result && result.length>2){
                        this.district = result[2]
                    }
                }
            },
        },
        watch:{
            keyword: function(newvalue, oldvalue){
                console.log(newvalue)
                console.log(oldvalue)
                this.answer = '加载中...'
                // 定时器
                setTimeout(() => {
                    this.answer = newvalue
                }, 1000);
            }
        }
    })
</script>
```
## 表单输入绑定
v-model指定可以实现表单值与属性的双向绑定。即表单元素中更改了值会自动的更新属性中的值，属性中的值更新了会自动更新表单中的值。

绑定的属性和事件：
v-model在内部为不同的输入元素使用不同的属性并抛出不同的事件：

1. text和textarea元素使用value属性和input事件。
2. checkbox和radio使用checked属性和change事件。
3. select字段将value作为prop并将change作为事件。

#### 修饰符
.lazy

在默认情况下，v-model在每次input事件触发后将输入框的值与数据进行同步 (除了上述输入法组合文字时)。你可以添加lazy修饰符，从而转变为使用change事件进行同步

.number

如果想自动将用户的输入值转为数值类型，可以给v-model添加number修饰符

.trim

如果要自动过滤用户输入的首尾空白字符，可以给 v-model 添加 trim 修饰符

下方代码参考:06表单输入绑定.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>bind_learn</title>
</head>
<body>
    <div id="app">
        <!-- v-model:value="xxx"的简写形式是v-model="xxx" -->
        <h1>textarea绑定</h1>
        <span >输入内容是:</span>
        <p>{{wbk}}</p>
        <textarea name="wbk" v-model='wbk' cols="30" rows="10"></textarea>

        <h1>checkbox绑定</h1>
        <input type="checkbox" value="jack" v-model="mname">
        <label for="jacl">jack</label>
        <input type="checkbox" value="john" v-model="mname">
        <label for="">john</label>
        <input type="checkbox" value="evan" v-model="mname">
        <label for="">evan</label>
        <br>
        <span>checked name: {{ mname }}</span>

        <h1>radio绑定</h1>
        <input type="radio" value="man" v-model:value='gender'>
        <label for="">man</label>
        <input type="radio" value="female" v-model:value='gender'>
        <label for="">female</label>
        <p style="white-space: pre-wrap;">{{gender}}</p>

        <h1>select绑定</h1>
        <select name="" id="" v-model="choose">
            <option disabled value="">请选择</option>
            <option value="1">A</option>
            <option value="B">B</option>
            <option value="C">C</option>
        </select>
        <p>HERE: {{choose}}</p>

        <h1>修饰符</h1>
        <input type="text" v-model.lazy.number.trim="modify">
        <p>out: {{modify}}</p>
    </div>
</body>
</html>

<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script>
    new Vue({
        el: '#app',
        data: {
            wbk: "",
            mname: [],
            gender: '',
            choose: '',
            modify: ''
        }
    })
</script>
```
## 自定义组件
有时候有一组html结构的代码，并且这个上面可能还绑定了事件。然后这段代码可能有多个地方都被使用到了，如果都是拷贝来拷贝去，很多代码都是重复的，包括事件部分的代码都是重复的。那么这时候我们就可以把这些代码封装成一个组件，以后在使用的时候就跟使用普通的html元素一样，拿过来用就可以了。

下方代码参考:07自定义组件.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <ohh></ohh>
        <ohh></ohh>
        <ohh></ohh>
    </div>
</body>
</html>

<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script>
    // ohh是自定义组件名，template是自定义组件的模板
    // 在自定义组建中，如果需要返回数据，是函数的形式，return返回的是对象
    Vue.component('ohh', {
        template: '<button @click="count += 1">点击了{{count}}次</button>',
        data: function(){
            return {
                count: 0
            }
        }
    });
    new Vue({
        el: '#app',
        data: {

        }
    })
</script>
```
以上我们创建了一个叫做ohh的组件，这个组件实现了能够记录点击了多少次按钮的功能。后期如果我们想要使用，就直接通过ohh使用就可以了。然后因为组件是可复用的Vue实例，所以它们与new Vue接收相同的选项，例如data、computed、watch、methods以及生命周期钩子等。仅有的例外是像el这样根实例特有的选项。另外需要注意的是：组件中的data必须为一个函数！

## 给自定义组件添加属性
像原始的html元素都有自己的一些属性，而我们自己创建的组件，也可以通过prop来添加自己的属性。这样别人在使用你创建的组件的时候就可以传递不同的参数了。

注意：如果自定义的组件中，会出现很多html元素，那么根元素必须只能有一个，其余的元素必须包含在这个根元素中。

下方代码参考:08给组件添加属性.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <!-- <blog-post ></blog-post> -->
        <blog-post :books="books"></blog-post>
    </div>
</body>
</html>

<script src="https://cdn.jsdelivr.net/npm/vue"></script>

<script>
    Vue.component('blog-post', {
        // 给自定义组件添加属性
        props: ['books'],
        // 多行用``来包裹模板，模板内根元素必须只有一个
        template: `
        <table>
            <tr>
                <th>序号</th>
                <th>标题</th>
            </tr>
            <tr v-for="(book,index) in books" :value="books">
                <td>{{index+1}}</td>
                <td>{{book}}</td>
            </tr>
            <tr></tr>
        </table>
        `
    })
    new Vue({
        el:"#app",
        data: {
            books: ['python', 'java', 'php']
        }
    })
</script>
```
## 子组件事件和传递事件到父组件
子组件中添加事件跟之前的方式是一样的，然后如果发生某个事件后想要通知父组件，那么可以使用this.$emit函数来实现。

下方代码参考:09传递事件.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <book-list v-for="book in books" :ok="book" v-on:father="solve">

        </book-list>
        <div v-for="c in cbook">
            {{c}}
        </div>
    </div>
</body>
</html>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    Vue.component('book-list', {
        props: ['ok'],
        template: `
        <div>
            <span>{{ok.title}}</span>
            <input type="checkbox" @click="oncheck">
        </div>
        `,
        methods: {
            oncheck: function(){
                // console.log(123)
                this.$emit('father', this.ok.title)
            }
        }
    })
    new Vue({
        el: '#app',
        data: {
            books: [
                {"title":"钢铁是怎样练成的？","id":1},
                {"title":"AI会毁灭人类吗？","id":2},
                {"title":"如何学好Vue！","id":3},
            ],
            cbook: [],
        },
        methods: {
            solve: function(oks){
                // console.log(ok)
                // this.cbook.push(ok)
                var index = this.cbook.indexOf(oks)
                if(index >= 0){
                    this.cbook.splice(index,1)
                }else{
                    this.cbook.push(oks)
                }

            }
        }

    })
</script>
```
## 自定义组件v-model
一个组件上的v-model默认会利用名为value的prop(属性)和名为input的事件，但是像单选框、复选框等类型的输入控件可能会将value特性用于不同的目的。这时候我们可以在定义组件的时候，通过设置model选项可以用来实现不同的处理方式.

下方代码参考:10自定义组件v-model.html
```html
<!DOCTYPE html>
<html lang="en">
<head>
    <meta charset="UTF-8">
    <meta name="viewport" content="width=device-width, initial-scale=1.0">
    <title>Document</title>
</head>
<body>
    <div id="app">
        <stepper v-model:value="fcount"></stepper>
    </div>
</body>
</html>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    Vue.component('stepper',{
        // props定义的属性是给外面调用组件时使用的
        props: ["count"],
        model:{
            // event代表什么情况下触发v-model行为，这里是点击sub | add会触发
            event: 'hi',
            // 使用v-model时，修改的属性
            prop: 'count'
        },
        template:`
        <div>
            <button @click="sub">-</button>
            <span>{{count}}</span>
            <button @click="add">+</button>
        </div>
        `,
        methods:{
            sub:function(){
                this.$emit("hi", this.count-1)
            },
            add:function(){
                this.$emit("hi", this.count+1)
            }
        }
    });
    new Vue({
        el:'#app',
        data:{
            fcount: 0
        },
    })
</script>
```
其中的props定义的属性分别是给外面调用组件的时候使用的。model中定义的prop:'count'是告诉后面使用v-model的时候，要修改哪个属性；event:'count-changed'是告诉v-model，后面触发哪个事件的时候要修改属性。

## 插槽
我们定义完一个组件后，可能在使用的时候还需要往这个组件中插入新的元素或者文本。这时候就可以使用插槽来实现。

下方代码参考:11插槽.html
```html
<body>
    <div id="app">
        <nva-link :rew="url">
            
            <template v-slot:1>baidu</template>
            <template>不给name属性我不会显示</template>
        </nva-link>
    </div>
</body>
</html>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    Vue.component('nva-link', {
        props: ['rew'],
        template: `
        <a :href="rew">
            <div>
                <slot name='myname'>{{myname}}</slot>
            </div>
            <div>
            <slot name='1'></slot>
            </div>
            <div>
            <slot name='2'></slot>
            </div>
        </a>
        `,
        data: function(){
            return {
                myname:"shell"
            }
        }
    })
    new Vue({
        el: '#app',
        data: {
            url: "https://www.baidu.com/"
        }
    })
</script>
```
## 插槽的作用域
下方代码参考:12插槽作用域.html
```html
<body>
    <div id="app">
        <container>
            <template v-slot:header="headerProps">header: {{headerProps.value}}</template>
            <template v-slot:footer="whatever">footer: {{whatever.value}}</template>
        </container>
    </div>
</body>
</html>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    Vue.component('container', {
        template: `
        <div>
            <div>
                <slot name="header" :value='navs'></slot>
            </div>
            <div>
                <slot name="footer" :value='address'></slot>
            </div>
        </div>
        `,
        data: function(){
            return {
                navs: ['1', '2', '3'],
                address: 'GD'
            }
        }
    })
    new Vue({
        el: '#app',
        data: {

        }
    })
</script>
```

## 生命周期函数
下方代码参考:13生命周期函数.html
```html
<body>
    <div id="app">
        <p id="username">{{username}}</p>
        <input type="text" v-model='username'>
        <error-info :error='message' v-if="message"></error-info>
        <button @click="Dmessage">删除错误</button>
    </div>
</body>
</html>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    Vue.component('error-info', {
        props: ['error'],
        template:'<p style="color:red">{{error}}</p>',
        // 7.vue实例或者是组件在被销毁之前执行的函数。在这一个函数中vue或者组件中所有
        // 的属性都是可以使用的。
        beforeDestroy(){
            console.log('---beforeDestroy---')
            console.log('删除前')
            console.log('---beforeDestroy---')
        },
        // 8.destroyed:Vue实例或者组件被销毁后执行的，此时vue实例上所有东西都会解绑
        // 所有事件都会被移除，所有子元素都会被销毁。
    })

    new Vue({
        // 1、beforeCreate: vue或组件刚刚实例化，data,methods都还没有被创建
        beforeCreate(){
            console.log("---beforeCreate---")
            console.log(this.username)
            console.log(this.demo)
            console.log("---beforeCreate---")
        },
        el: '#app',
        data: {
            username: 'shell',
            message: '错误信息'
        },
        methods: {
            demo: function(){
                return "hello world"
            },
            Dmessage: function(){
                this.message = ''
            }
        },
        // 2、此时data和methods已经被创建，但模板还没有被编译
        created(){
            console.log("---created---")
            console.log(this.username)
            console.log(this.demo)
            console.log("---created---")
        },
        // 3、此时模板已经被编译了，但是并没有被挂载到网页中
        beforeMount(){
            console.log('---beforeMount---')
            console.log(document.getElementById('username').innerText)
            console.log('---beforeMount---')
        },
        // 4、模板代码已经被加载到网页中了，此时创建期间所有事情都已经准备好了，网页开始运行了
        mounted(){
            console.log('---mount---')
            console.log(document.getElementById('username').innerText)
            console.log('---mount---')
        },
        // 5、在网页运行期间，data中的数据可能会进行更新。在这个阶段，数据只在data中更新了
        // 还没有在模板中更新，因此网页中显示的还是之前的数据。
        beforeUpdate(){
            console.log('---beforeUpdate---')
            console.log(document.getElementById('username').innerText)
            console.log('---beforeUpdate---')
        },
        // 6.此时数据在data中更新了，在网页中也更新了
        updated(){
            console.log('---updata---')
            console.log(document.getElementById('username').innerText)
            console.log('---updata---')
        },

        
    })
</script>
```

## 过滤器
过滤器就是数据在真正渲染到页面中的时候，可以使用这个过滤器进行一些处理，把最终处理的结果渲染到网页中。

过滤器使用：
过滤器可以用在两个地方：双花括号插值**和v-bind表达式 (后者从2.1.0+开始支持)。过滤器应该被添加在JavaScript表达式的尾部，由“管道”符号指示.

下方代码参考:14过滤器.html
```html
</body>
</html>
<script src="https://cdn.jsdelivr.net/npm/vue"></script>
<script>
    // 使用过滤器的方法1
    // Vue.filter('choose', function(value){
        // var newValue = value.replace('  ', '')
        // return newValue
    // })
    new Vue({
        el: '#app',
        data: {
            message: '过滤 空格'
        },
        // 使用过滤器的方法2
        filters: {
            choose: function(value){
                // if (value) return '111'
                // newValue = value.toString()
                // return newValue.charAt(0).toUpperCase() + value.slice(1)
                return value.replace(' ', '')
            }
        }
    })
</script>
```

## vue-router 路由
1. 基本使用---参考"15路由的基本使用.html"
2. 动态路由---参考"16路由-动态.html"
3. 路由嵌套---参考"17路由嵌套.html"
4. 编程式导航---参考"18编程式导航.html"
5. 命名路由&命名视图---参考"19重命名视图.html"