[toc]
# vue.js 框架的学习
[vue.js文档链接](https://cn.vuejs.org/v2/guide/syntax.html)

 Vue两大核心思想，组件化和数据驱动，组件化就是将一个整体合理拆分为一个一个小块（组件），组件可重复使用，数据驱动是前端的未来发展方向，释放了对DOM的操作，让DOM随着数据的变化自然而然的变化（尤神原话），不必过多的关注DOM，只需要将数据组织好即可。

## 安装vue
安装vue 通过终端npm install vue下载安装		
或者通过https://cdn.jsdelivr.net/npm/vue/dist/vue.js 外部引入

```js
<script src="https://cdn.jsdelivr.net/npm/vue/dist/vue.js"></script>
```
MVVM : MVC改进版---就是将其中的View 的状态和行为抽象化，让我们将视图 UI 和业务逻辑分开		
//mvvm m:data; v:id 对应的HTML; vm:app;

## 创建第一个vue
首先现在body里绑定div

```js
<div id="app">
<!--v-model 绑定并联动数据-->
    <input type="text" v-model="message">
    message:{{message}}
    <!--<button onclick="changeData()">改变数据</button>-->
</div>
```
当input输入内容时,外面的message:后的内容会跟着发生变化

然后在script里声明并创建vue

```js
//创建一个vue
var app = new Vue({
    //绑定视图 作用域是ID对应的子视图
	//指任何操作都必须在绑定的div内
    el:'#app',
    data:{//数据
        message:'hello vue!'
    }
});
app.message = "hello word";
app.message = "hello"; //后赋值的覆盖以前赋值的
function changeData() {
    app.message = "data"; //app.data.message  点击改变数据
}
```

## v-方法名 属于vue的操作方法
## 第一天学习 v-bind, v-if, v-show, v-for, v-on

v-bind:     
```
作用：v-bind绑定页面中的元素属性。例如：a的href属性，img的src、alt和title属性。        
语法：v-bind:元素的属性名 = “data中键名” 
```
v-if:       
```
作用：判断是否加载固定的内容。如果为真，则加载；为假时，则不加载。      
用处：用在权限管理，页面条件加载        
语法：v-if=”判断表达式”     
特点：控制元素插进来或者删除，而不是隐藏。      
v-if与v-show的区别：        
一般来说，v-if有更高的切换消耗，安全性更高，而v-show有更多的初始化渲染消耗。因此，如果需要频繁切换而对安全性无要求，使用v-show。如果在运行时，条件不可能改变，则使用v-if较好。      
```
v-show:     
```
作用：通过判断，是否显示该内容。如果值为true，则显示。否则就隐藏。
语法：v-show=”判断表达式”
特点：元素会始终渲染在DOM中，只是被设置了display:none
```
v-for:      
```
作用：控制html元素中的循环，实现诗句列表的生成。
用法：如下例子
view:
v-for=”item in 集合”
item: 集合的子项
集合：被遍历的集合，通常为数组。
用处：写在谁上，谁循环。
```
v-on:
```
作用：对页面中的事件进行绑定
语法： v-on:事件类型=“事件处理函数名”
缩写： @事件类型=“事件处理函数名”
```

例子:       
body里的div绑定

```js
<div id="app">
    <!--v-bind 绑定属性 简写:属性名。可以直接不写v-bind-->
    <a :href="url">百度</a> 

    <!--v-if 值 boolean类型 true:显示  false:不显示 (是否渲染)-->
    <div v-if="isShow">是否显示</div>

    <!--v-show 是否显示对应DIV里的内容 true:显示  false:不显示-->
    <div v-show="isShow">阿斯顿</div>

    <ul>
        <!--v-for 循环标签 data是循环对象的元素 listFor循环对象 data或listFor名字都可以自定义-->
        <li v-for="data in listFor">
            <div>名字:{{data.name}}</div>
            <div>年龄:{{data.age}}</div>
        </li>
    </ul>

    <!--v-on 绑定事件 事件定义在实例的method属性里 简写@click-->
    <button v-on:click="changeShow">按钮</button>
    <button @click="changeText">改名字</button>
</div>
```

script里的代码
```js
var data = {
        name:'zhangsan',
        age:18,

        //v-bind 绑定属性 简写:属性名。可以直接不写v-bind
        //在data里给url设置的路径传给v-bind所绑定的属性
        url:"http://www.baidu.com", //标签里的属性不能用{()}

        //v-if 值 boolean类型 true:显示  false:不显示 (是否渲染)
        //v-show 是否显示对应DIV里的内容 true:显示  false:不显示
        isShow:false,

        //v-for 循环标签
        listFor:[
            {
                name:'张三',
                age:18
            },{
                name:'李四',
                age:16
            },{
                name:'阿斯顿',
                age:19
            }
        ]


    };
    // Object.freeze(data);//阻止数据更新
    var app = new Vue({
        el:'#app',
        data:data, //初始化赋值
        //v-on 绑定事件 事件定义在实例的method属性里 简写@click
        methods:{
            changeShow:function () {
                this.isShow = !this.isShow;
            },
            changeText:function () {
                this.name = "规划局";
            }
        }
    });
```
## 第二天学习 v-html, 计算属性 取值器 赋值器改数值, 大小写转换, watch监听器, :class, :style, v-if, v-else, v-else-if, v-for, v-model, 过滤器

### v-html, 计算属性 取值器 赋值器改数值, 大小写转换, watch监听器      
v-html:
```
作用：操作元素中的html
```
计算属性 取值器 赋值器改数值:
```
进行逻辑计算的区块 任何涉及到计算的动作请在这里面书写      
数据加载完成之后
计算属性 data里没有声明 是计算后得到的  拦截器可以实现类似功能
computed区块里定义的都是属性  在这里goods是一个属性,不是方法
取值器, computed默认只有取值器
赋值器 在需要时,我们可以手动启用赋值器
```
大小写转换:
```
调用方法即可,看如下例子
```
watch监听器:
```
监听器区块  当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。
```
body里的div绑定
```js
<div id="app">
    <!--<div>{{msg}}</div>-->
    <div>{{html}}</div>
    <!--v-html  向调用 html 的对象里嵌套html标签-->
    <div v-html="html"></div>

    <!--算数计算不推荐的方法-->
    <div>¥{{price + 6}}</div>
    <!--算数计算函数调用方法-->
    <div>{{goods}}</div>

    <!--变成大写,不推荐这个方法-->
    <div>{{firstName.toUpperCase()}}</div>
    <!--变成大写,函数调用方法-->
    <!--<div>{{showFirstName}}</div>-->
    <!--methods方法函数调用-->
    <div>{{showFirstName2("san")}}</div>
    <!--全名-->
    <div>{{fullName}}</div>

    <!--watch 监听器-->
    <input type="text" v-model="message">
    <div>{{msg}}</div>
    <div>{{message}}</div>
</div>
```
script里的代码
```js
/*
    1,v-html  向调用 html 的对象里嵌套html标签
    2,计算属性 data里没有声明 是计算后得到的
    在div里直接调用计算函数即可
        价格100   $100   ¥100
        asdfgh  ASDFGH Asdfgh
    */

    //vm:app
    var app = new Vue({
        el:'#app',
        data:{
            html:'<span>这是一个span标签</span>',
            price:100, //¥100  包含快递费
            firstName:'zhang',
            lastName:'san',
            msg:'666',
            message:''
        },

        //进行逻辑计算的区块 任何涉及到计算的动作请在这里面书写
        computed:{ //数据加载完成之后
            //计算属性 data里没有声明 是计算后得到的  拦截器可以实现类似功能
            goods:function () { ////computed区块里定义的都是属性  在这里goods是一个属性,不是方法
                return '¥' + (this.price + 6);
            },
            /*fullName:function () {
                return this.firstName + " " + this.lastName;
            },*/
            //计算属性默认值有取值器
            fullName:{
                //取值器, computed默认只有取值器
                get:function () {
                    return this.firstName + " " + this.lastName;
                },
                //赋值器 在需要时,我们可以手动启用赋值器
                set:function (newName) {
                    // this.fullName = newName; //报错 进入死循环,栈溢出
                    var names = newName.split(' ');
                    this.firstName = names[0];
                    this.lastName = names[names.length - 1];
                }
            }
            /*showFirstName:function () {
                return this.firstName.toUpperCase();
            }*/
        },
        methods:{//方法区块, showFirstName是一个方法
            //尽管 computed和methods都可达到同样的效果,但是两者有些区别
            //computed会缓存第一次调用属性得到的结果,在再次调用属性时,如果数据没有发生改变则直接返回缓存的结果
            //如果数据发生改变则重新执行函数.
            //而对于methods而言,每次调用的都是方法,每调用一次方法则执行一次函数. 如果数据量很大则计算量也很大
            //@click="showFirstName('bbb')" 另一种调用方式
            showFirstName2:function (name) {
                //@click="showFirstName2('san')"
                return this.firstName.toUpperCase() + " " + name;
            }
        },
        watch:{ //监听器区块  当需要在数据变化时执行异步或开销较大的操作时，这个方式是最有用的。
            message:function (newvalue,oldvalue) {
                // this.message = value + 1;
                //可以实现数据绑定和实时更改
                this.msg = newvalue;
                //打印显示新的和旧的数据
                console.log(newvalue + " " + oldvalue);
            }
        }
    })
    // app.msg = "这是一条消息"; 后期无法添加属性
    // app.fullName("li si"); //会报错 fullName 不是方法

    //赋值改名
    app.fullName = "狗 蛋";
```

----------------------------分割线----------------------------     
### :class, :style 
:class :
```
添加class类名
```
:style :
```
添加内联样式
```
body里的div绑定
```js
<div id="app">
    <!--添加class类名-->
    <!--方法1-->
    <div :class="{active:isActive,'img-text':has}">
        <!--方法2-->
        <div :class="classObj"></div>
        <!--方法3-->
        <div :class="[class1,class2]"></div>
        <!--方法4 嵌套写法-->
        <div :class="[class1,{div3:has}]"></div>
        <!--方法5-->
        <div :class="[isActive ? class1 : class2,class3]"></div>

        <!--:style 内联样式  方法1-->
        <div :style="{color:redColor,fontSize:font}">方式方法</div>
        <!--内联样式对象写法 值得推荐  方法2-->
        <div :style="styleObj">内联样式对象写法</div>
        <!--内联样式  方法3-->
        <div :style="[baseStyle,headerStyle]">方法3</div>
    </div>
</div>
```

在script里的代码
```js
/*
        :class  在html标签内添加class类名
    */
    var app = new Vue({
        el:'#app',
        data:{
            //方法1
            isActive:false, //false 不显示这个class 类名
            has:true, //true 显示这个class 类名
            //方法2
            classObj:{
                active:true, //false 不显示这个class 类名
                'img-has':true, //true 显示这个class 类名
            },
            //方法3
            class1:'div1',
            class2:'div2',
            class3:'div4',

            //:style 内联样式
            //方法1
            redColor:'red',
            font:'30px',
            //方法2
            styleObj:{
                color:'blue',
                fontSize:'50px',
                background:'pink',
            },
            //方法3
            baseStyle:{
                color:'red'
            },
            headerStyle:{ //.vue
                background:'green'
            }
        }
    })
```
----------------------------分割线----------------------------     
### v-if, v-else, v-else-if, v-for     
v-if:
```
作用：判断是否加载固定的内容。如果为真，则加载；为假时，则不加载。
用处：用在权限管理，页面条件加载
语法：v-if=”判断表达式”
特点：控制元素插进来或者删除，而不是隐藏。
v-if与v-show的区别：
一般来说，v-if有更高的切换消耗，安全性更高，而v-show有更多的初始化渲染消耗。因此，如果需要频繁切换而对安全性无要求，使用v-show。如果在运行时，条件不可能改变，则使用v-if较好。
```
v-else:
```
v-else必须紧跟在v-if后面，否则他不能被识别。表示：当v-if的条件不成立的时候执行。
```
v-else-if:
```
和v-if配合使用
```
v-for:
```
作用：控制html元素中的循环，实现诗句列表的生成。
用法：
view:
v-for=”item in 集合”
item: 集合的子项
集合：被遍历的集合，通常为数组。
用处：写在谁上，谁循环。
```
在body里的div绑定
```js
<div id="app">
    <div v-if="type === 'loading'">
        现在是正在加载
    </div>
    <!--<div v-else>
        加载完成
    </div>-->
    <div v-else-if="type === 'loaded'">
        加载完成
    </div>
    <div v-else-if="type === 'destory'">
        销毁
    </div>
    <div v-else>
        404
    </div>

    <!--
    vue有一个特性,值可以重复利用. 在input输入值后,切换input时,值依然在,不销毁.
    但有好也有坏
    取消数值重复利用是直接加 key ,让 key 不一样就可以
    -->
    <div v-if="type==='loading'">
        <input type="text" placeholder="请输入姓名..." key="input1">
    </div>
    <div v-else>
        <input type="text" placeholder="请输入年龄..." key="input2">
    </div>
    <button @click="changeType">切换</button>

    <ul>
        <!--{{data.element}}-->
        <!--在v-for作用块内 可以访问随意随意访问父级数据,但是父级不能访问 v-for 生成的数据,比如在父级使用 {{data.element}} 会报错-->
        <li v-for="(data,index) in list" :index="index">
            {{type}}
            {{data.element}}
            <!--index 自动添加编号-->
            <!--:index="index(自定义名字)" 自动给标签内联上添加 index 编号-->
            <!--:index上编号需要和v-for="(data,index) in list"配合使用-->
            {{index}}
        </li>
        <!--{{data.element}}-->
    </ul>

    <ul>
        <li v-for="(value,key,index) in obj">
            <!--key 遍历对象,显示key值和value值,并且自动添加编号-->
            {{key}}
            {{value}}
            {{index}}
        </li>
    </ul>

    <ul>
        <li v-for="num in nums">
            {{num}}
        </li>
    </ul>
    <button @click="changeNum">改变数值</button>
    <button @click="changeName('狗蛋')">改变名字</button>
</div>
```
在script里的代码
```js
var app = new Vue({
        el:'#app',
        data:{
            type:'loading',
            list:[
                {
                    element:'el1'
                },
                {
                    element:'el2'
                },
                {
                    element:'el3'
                },
                {
                    element:'el4'
                }
            ],
            obj:{
                name:'shangsan',
                age:18,
                sex:'男'
            },
            nums:[1,2,3,4,5,6,7]
        },
        methods:{
            changeType:function () {
                this.type = 'loaded';
            },
            changeNum:function () {
                // this.nums[1] = 9; //这种方式虽然更改了但不能显示
                // console.log(this.nums[1]);

                //更新数组 Vue.set 和app.$set 一样的
                // 括号内(更新对象,更新位置,更新数值)
                // Vue.set(app.nums,1,9); //第一种写法
                app.$set(app.nums,1,9); //第二种写法
                //添加数值
                // this.nums.push(9)
            },
            changeName:function (name) {
                app.$set(app.obj,"name",name) //改name的value值
            }

        }
    });
```
----------------------------分割线----------------------------      
### v-model, 过滤器     
v-model:
```
作用：接受用户输入的一些数据，直接就可以将这些数据挂在到data属性上。这样就产生了双向的数据绑定（当业务模型中的数据发生变化时，用户界面中的数据会发生变化；当用户界面中的数据变化时，业务模型中的数据也会发生变化）。
语法：v-model = “data中的键名”
在data中，最好也要定义这个属性，不然会报错。
```
过滤器:
```
过滤器是一个通过输入数据，能够及时对数据进行处理并返回一个数据结果的简单函数。
```
在body里的div绑定
```js
<div id="app">
    <!--v-model 绑定并联动数据-->
    <input type="checkbox" id="checkbox" v-model="checked">
    {{checked}}

    <div>
        <!--
        这波操作,你选中哪个,就自动把哪个 value 值写入 names 数组里
        v-model="names" 绑定空数组
        -->
        <input type="checkbox" id="zhangsan" value="zhangsan" v-model="names">
        <label for="zhangsan">zhangsan</label>
        <br>
        <input type="checkbox" id="lisi" value="lisi" v-model="names">
        <label for="lisi">lisi</label>
        <br>
        <input type="checkbox" id="wangwu" value="wangwu" v-model="names">
        <label for="wangwu">wangwu</label>
        <br>
        names:{{names}}
    </div>

    <div>
        <!--与上面类似-->
        <input type="radio" value="goudan1" name="goudan1" v-model="name">goudan1 <br>
        <input type="radio" value="goudan2" name="goudan2" v-model="name">goudan2 <br>
        <input type="radio" value="goudan3" name="goudan3" v-model="name">goudan3 <br>
        name:{{name}}
    </div>

    <div>
        <!--同上类似-->
        <!--multiple 多选-->
        <select name="" id="" v-model="selected" multiple>
            <option value="">请选择...</option>
            <option>A</option>
            <option>B</option>
            <option>C</option>
            <option>D</option>
        </select>
        select:{{selected}}
    </div>
    <!--调用upperCase方法,变成大写-->
    {{message | upperCase}}

</div>
```
script里的代码
```js
var app = new Vue({
        el:'#app',
        data:{
            checked:false,
            names:[],
            name:'',
            selected:[],
            message:'sdfsdfdf'
        },
        // 过滤器
        // 过滤器是一个通过输入数据，能够及时对数据进行处理并返回一个数据结果的简单函数。
        filters:{
            upperCase:function (value) {
                if (!value) return '';
                value = value.toString();
                return value.toUpperCase();
            }
        }
    })
```

## 第三天学习 生命周期, 全局注册组件, 局部注册组件, DOM模板解析, data必须是函数, prop, 动态prop, 自定义事件

### 生命周期
Vue实例从创建到销毁的过程，就是生命周期。详细来说也就是从开始创建、初始化数据、编译模板、挂载Dom、渲染→更新→渲染、卸载等一系列过程。      
![Alt text][lifecycle] 

如上图,Vue提供给我们的钩子为上图的红色的文字

例子:       
body里的div绑定:
```js
<div id="app">
    <div>{{message}}</div>
    <button @click="clicked">点击</button>
    <button @click="changeMessage">改变数值</button>
</div>
```
在script里的代码:
```js
var app = new Vue({
        el:'#app',
        data:{
            message:'hello vue!'
        },
        methods:{
            clicked:function () {
                this.$destroy(); //销毁实例
                /*this.message = "歼星舰"; //更新实例
                console.log('我是一个点击事件');*/
            },
            changeMessage:function () { //销毁之前会更该数值,但当销毁之后,就无法进行更改数值操作
                this.message = '奥术大师多';
            }
        },
        //在实例初始化之后，数据观测(data observer) 和 event/watcher 事件配置之前被调用。
        //告诉使用者创建Vue对象进度状态,分成创建之前和创建之后,分步展示
        beforeCreate:function () {
            console.log('创建之前');
            console.log(this.message); //创建之前,没有显示
            console.log(this.$el); //创建之前,没有显示
            console.log(this.clicked);
        },
        //实例已经创建完成之后被调用。在这一步，实例已完成以下的配置：数据观测(data observer)，属性和方法的运算， watch/event 事件回调。
        //主要应用：调用数据，调用方法，调用异步函数
        created:function () {
            console.log('已经创建');
            console.log(this.message); //正在创建,有显示 hello vue!
            console.log(this.$el); //正在创建,没有显示
            console.log(this.clicked); //正在创建,有显示 clicked的函数
            //数据处理,不能放方法
            //获取数据从服务器, 不能操作

        },
        //在挂载开始之前被调用：相关的 render 函数（模板）首次被调用。
        //告诉使用者挂载视图进度状态,分为挂载之前和挂载完成两个,分步展示
        beforeMount:function () {
            console.log('挂载之前');
            console.log(this.$el); //挂载之前,有显示$el绑定的对象
            //开始对视图操作
        },
        //el 被新创建的 vm.$el 替换，并挂载到实例上去之后调用该钩子。 
        mounted:function () {
            console.log('挂载完成');
            console.log(this.$el); //挂载完成,有显示$el绑定的对象,并且还会显示绑定对象的内容
            //ajax请求在这里进行,这是视图和数据都初始化完成
        },
        //数据更新时调用，发生在虚拟 DOM 重新渲染和打补丁之前。 你可以在这个钩子中进一步地更改状态，这不会触发附加的重渲染过程。 
        //当我们更改Vue的任何数据，都会触发该函数
        //更新,当内容发生变化时自动调用  分两个状态,更新之前,更新完成
        beforeUpdate:function () {
            console.log("更新之前");
            console.log(this.$el.innerHTML); //显示更新之前内容
        },
        //由于数据更改导致的虚拟 DOM 重新渲染和打补丁，在这之后会调用该钩子。 
        //当这个钩子被调用时，组件 DOM 已经更新，所以你现在可以执行依赖于 DOM 的操作。然而在大多数情况下，你应该避免在此期间更改状态，因为这可能会导致更新无限循环。 
        //该钩子在服务器端渲染期间不被调用。
        //数据更新就会触发（vue所有的数据只有有更新就会触发）,如果想数据一遍就做统一的处理，可以用这个，如果想对不同数据的更新做不同的处理可以用nextTick，或者是watch进行监听
        updated:function () {
            console.log("更新完成");
            console.log(this.$el.innerHTML); //显示更新之后内容
        },
        //实例销毁之前调用。在这一步，实例仍然完全可用。
        //确认是否成功销毁对象
        beforeDestroy:function () {
            console.log('销毁之前');
        },
        //Vue 实例销毁后调用。调用后，Vue 实例指示的所有东西都会解绑定，所有的事件监听器会被移除，所有的子实例也会被销毁。该钩子在服务器端渲染期间不被调用。
        destroyed:function () {
            console.log('销毁完成');
        }

    })
```

### 全局注册组件
全局组件  可以一个组件放到多个实例对象里使用        
参数1 组件名        
参数2 选项   模板   字符串模板   根元素只能有一个,只能往里写,不能往下写,只能一个套一个

在body里的代码:
```js
<div id="app">
    <my-component></my-component>
</div>
<div id="app2">
    <my-component></my-component>
</div>
```

在script里的代码:
```js
Vue.component('my-component',{
        template:'<div><h1 class="h1">我是一个组件</h1><h2>我是👌</h2></div>'
    })

    var app = new Vue({
        el:'#app',
        data:{

        }
    })

    var app2 = new Vue({
        el:'#app2',
        data:{

        }
    })
```

### 局部注册组件
局部组件:只在当前vue实例里有效

在body里的代码:
```js
<div id="app">
    <my-components></my-components>
    <table>
        <my-th></my-th>
        <my-tr></my-tr>
        <my-tr></my-tr>
        <my-tr></my-tr>
        <!--可以用is引入-->
        <tr is="my-tr"></tr>
    </table>
</div>
```

在script里的代码:
```js
var app = new Vue({
    el:'#app',
    components:{
        'my-components':{
            template:'<h1>我是一个局部组件</h1>'
        },
        'my-th':{
            template:'<th>我是表头</th>'
        },
        'my-tr':{
            template:'<tr>我是tr123</tr>'
        }
    }
})
```

### DOM模板解析
在body里的代码:
```js
<div id="app">
    <table>
        <my-th></my-th>
        <my-tr></my-tr>
        <my-tr></my-tr>
        <my-tr></my-tr>
        <!--可以用is引入-->
        <tr is="my-tr"></tr>
    </table>
    <my-comp></my-comp>
</div>
```

在script里的代码:
```js
<script type="text/x-template" id="temp1">
    <div>
        <h1>h1</h1>
        <h2>h2</h2>
        <a href="http://www.baidu.com">百度</a>
    </div>
</script>

<template id="temp2">
    <div>div</div>
</template>

<script type="application/javascript">
    /*
    局部组件
      只在当前vue实例里有效
    */
    var app = new Vue({
        el:'#app',
        components:{
            'my-th':{
                template:'<th>我是表头</th>'
            },
            'my-tr':{
                template:'<tr>我是tr123</tr>'
            },
            'my-comp':{
                template:'#temp1'
            }
        }
    })
</script>
```

### data必须时函数
在body里的代码:
```js
<div id="app">
    <my-comp></my-comp>
    <my-comp></my-comp>
    <my-comp></my-comp>
</div>
```
在script里的代码:
```js
<script type="application/javascript">
    /*
    局部组件
      只在当前vue实例里有效
    */
    /*var data = { //用这个写法的话,会导致点击按钮所有count都改变,因为在外面全局 data 属于唯一的
        message:'我是一个函数',
        count:0
    };*/

    var app = new Vue({
        el:'#app',
        components:{
            'my-comp':{ //模板
                template:'<div>{{count}}<button @click="count++">按钮</button></div>',
                /*data:{ //直接这么写会报错,data必须时函数,通过return返回
                    message:'我是一个函数'
                },*/
                //要想在组件内添加样式,for循环之类的,所需要的数据得如下写法,return返回数据
                data:function () {
                    return {
                        count:0
                    }
                },
                //可以用其他组件
                /*component:{

                },
                methods:{

                }*/
            }
        },
        data:{ //和上面的data没有关系,上面的data在 my-comp 的模板里
            count:10
        }
    })
</script>
```
### prop
组件实例的作用域是孤立的。这意味着不能(也不应该)在子组件的模板内直接引用父组件的数据。要让子组件使用父组件的数据，我们需要通过子组件的props选项。

prop 是单向绑定的：当父组件的属性变化时，将传导给子组件，但是不会反过来。这是为了防止子组件无意修改了父组件的状态。

每次父组件更新时，子组件的所有 prop 都会更新为最新值。这意味着你不应该在子组件内部改变 prop。      


在body里的代码:
```js
<div id="app">
    <!--myMessage 不区分大小写,所以要用这个应该写成 my-message 才行-->
    <my-comp my-message="hello vue~"></my-comp>
</div>
```
在script里的代码:
```js
<script type="application/javascript">
    var app = new Vue({
        el:'#app',
        components:{
            'my-comp':{ //模板
                template:'<div>{{myMessage}}</div>',
                //props和data一样, prop声明的值可以直接在模板中使用
                props:['myMessage'], //声明父级传入的数据,要放在组件里
                methods:{
                    changeMsg:function () {
                        // this.message = 'haha';
                    }
                }
            }
        }
    })
</script>
```

### 动态prop
在body里的代码:
```js
<div id="app">
    <!--myMessage 不区分大小写,所以要用这个应该写成 my-message 才行-->
    <my-comp :message="message" :number="number"></my-comp>
    <!--:message 里的message是props传入的message  item.message里的message是data里的message数据-->
    <my-comp :message="item.message" :number="item.number"></my-comp>
    <my-comp v-bind="item"></my-comp>
</div>
```

在script里的代码:
```js
<script type="application/javascript">
    /*
    1,动态props 使用v-bind与父级的data进行绑定
    2,字面量语法和动态语法区别  字面量语法: message='hello'
    直接字面量传入的是一个string类型

    prop 是单向传递,当父组件发生变化时传递给子组件
    但是反过来不会,子组件发生变化是prop不会传递
    */
    var app = new Vue({
        el:'#app',
        components:{
            'my-comp':{ //模板
                template:'<div>{{chMsg}} : {{number}} <button @click="changeMsg">更改</button></div>',
                //props和data一样, prop声明的值可以直接在模板中使用
                props:['message','number'], //声明父级传入的数据,要放在组件里
                methods:{
                    changeMsg:function () {
                        //this.message = 'haha'; //不建议这么更改,会出问题报错,在子组件更改了,外面的data没有更改,会导致错误
                        this.chMsg = 'haha'; //配合下面的定义属性重新赋值,改了后就没有问题
                    }
                },
                data:function () {
                    return {
                        //定义属性重新赋值
                        chMsg:this.message
                    }
                },
                /*computed:{
                    chMsg:function () {
                        return this.message + "haha";
                    }
                }*/
            }
        },
        data:{
            message:'消息',
            number:10,
            item:{
                message:'阿萨德',
                number:100
            }
        }
    })
</script>
```

### 自定义事件:
在body里的代码:
```js
<div id="app">
    <my-comp v-on:pass="countAdd"></my-comp>
    <my-comp v-on:pass="countAdd"></my-comp>
    <my-comp v-on:pass="countAdd"></my-comp>
    {{count}}
</div>
```
在script里的代码:
```js
<script type="application/javascript">
    var app = new Vue({
        el:'#app',
        components:{
            'my-comp':{ //模板
                template:'<div>{{count}}<button @click="changeMsg">更改</button></div>',
                //props和data一样, prop声明的值可以直接在模板中使用
                props:['message','number'], //声明父级传入的数据,要放在组件里
                methods:{
                    changeMsg:function () {
                        this.count++;
                        //向父级传递消息
                        this.$emit('pass',{message:'1211'});
                    }
                },
                data:function () {
                    return {
                        count:0

                    }
                }

            }
        },
        data:{
            count:0,
            // message:'消息',
            // number:10,
            item:{
                message:'阿萨德',
                number:100
            }
        },
        methods:{
            countAdd:function (msg) {
                this.count++;
                console.log(msg)
            }
        }
    })
</script>
```











[lifecycle]:data:image/png;base64,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