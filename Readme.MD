在vue中watch和created哪个先执行？为什么？
    1.如果 watch 设置了 immediate 为true  就是 watch先执行 ,否则就是 created；

    2.官网的生命周期图中，init reactivity（初始化校验）是晚于beforeCreate但是早于created的。
    watch加了immediate，应当同init reactivity周期一同执行，早于created。
    而正常的watch，则是mounted周期后触发data changes的周期执行，晚于created。

    2.1 watch 的一个特点是，最初绑定的时候是不会执行的，要等到 参数 改变时才执行监听计算。
    2.2 watch 中的 immediate 会让监听在初始值声明的时候去执行监听计算，否则就是 created 先执行



vue中mixins和extends有什么区别？
    1.mixins 能混入多个 mixin， 而 extends 只能 接收一个。
    2.extends 的优先级比 mixins高，会先执行。（最高的是 Vue.extend----创建组件的构造函数，为了复用）


vue 中父组件如何监听子组件的生命周期？
    1.使用hook钩子函数 
    2.在子组件生命周期中使用$emit('callback')触发父组件中的方法
                    http://cache.baiducontent.com/c?m=edR6uhJcwiDxiauZ3Z6KG4phuTP9lDI6wllZPsEn4Fz-optI2XXhFZU5bA9XlcZMhdWbaVv71AlHBZPWzBhLain9Zdm4iPMjzgcj2t9UkAy9ozlCRoInD_DEBElCaw_XXW8xciV3iUpbfWoOT9Wrnxyv4LLV7XbnjjBXKscCsH1uTwuyTMRCJEVU7i11-j4uhZGKx1TcX8AyaGPLFPqOpWTeTWkFXHA143SeQg_aLZm&p=cb3bcb16d9c102c312bd9b7b0e42&newp=8b2a9715d9c642b54baedf3d164c92695d0fc20e38d5db01298ffe0cc4241a1a1a3aecbf2c251002d0ce766c0ba54e59ebf733723d0034f1f689df08d2ecce7e&s=9517fd0bf8faa655&user=baidu&fm=sc&query=%C8%E7%BA%CE+%D7%E8%D6%B9+%D7%D3%D7%E9%BC%FE%B5%C4%C9%FA%C3%FC%D6%DC%C6%DA&qid=a402d1000003a230&p1=1


vue中mixins有什么使用场景？
    1.代码复用，扩充原有组件的方法。
    1.1一般一些有重复方法的组件，可以考虑抽一个mixin。或者是比如一些页面权限控制的内容，也可以考虑抽一个mixin
    

在vue中created与activated有什么区别？   ==========


在vue项目如何引入异步组件？
        
        延迟加载组件                            代码拆分/延迟加载/动态导入

        延迟加载    () => import('./components/Tooltip')
        eg:
        export default {
            components: {
                Tooltip: () => import('./components/Tooltip')
            }
        }

在vue项目中scss scoped穿透符>>>无效的解决方案有哪些？
    注释：vue引用了第三方组件，需要在组件中局部修改第三方组件的样式，而又不想去除scoped属性造成组件之间的样式污染。此时只能通过>>>，穿透scoped。
    1.有些Sass 之类的预处理器无法正确解析 >>>，（此时） 可以使用 /deep/ 或者 ::v-deep 操作符( >>> 的别名) 
        eg: /deep/.el-input{}       .a /deep/ .b {}
            ::v-deep .el-input{}    .a ::v-deep .b {}




为什么在v-for中的key不推荐使用随机数或者index呢？那要怎么使用才比较好呢？
    因为在插入数据或者删除数据的时候，会导致后面的数据的key绑定的index变化，进而导致从新渲染，效率会降低
    建议使用一个 唯一键值  进行标记





vue-loader在webpack编译流程中的哪个阶段？       =======
预渲染和SSR(服务端渲染)有什么区别？                 ========
你有用过预渲染技术吗？怎么做的？                 ========


使用vue如何判断页面是否编辑及编辑页面未保存离开时，给出弹窗提示
    路由守卫 beforeRouteLeave
    $watch  deep 深度监听，immediate 在初始化时就进行监听


vue的.sync修饰符可以用表达式吗？为什么？
    不行
    .sync修饰符的作用：用于实现父子组件数据的双向绑定 (语法糖)
    子组件添加: :child-value.sync ='value'。 Vue看到 .sync关键字会自动为子组件创建一个叫做 update:childValue或者update:child-value的事件。(这两种事件名都可以成功调用) 这个事件可以接受参数，并自动将参数赋给父组件的 value。

    .sync是一个语法糖，可拓展为一个自动更新父组件属性的v-on监听器。

    作者：没有鱼丸_b12f
    链接：https://www.jianshu.com/p/1d205355e2fb
    来源：简书
    著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。


v-if和v-show哪个优先级更高？
    v-for > v-if > v-show

如何批量引入组件？
    利用 webpack 的 require-context, 批量获取相关module

vue的v-for如何倒序输出？
    v-for="item in items.slice().reverse()"

如何在全局使用axios的实例呢？
    注册到 Vue 的原型上

v-show指令算是重排吗？
axios同时请求多个接口，如果当token过期时，怎么取消后面的请求？
    <!-- CancelToken -->
    axios.CancelToken 
     xhr.abort()


从0到1自己构架一个vue项目，说说有哪些步骤、哪些重要插件、目录结构你会怎么组织       ========
    vue creat axios拦截  代理配置 公共方法  utlis    引用相关组件

你知道vue的模板语法用的是哪个web模板引擎的吗？说说你对这模板引擎的理解=======
你知道v-model的原理吗？说说看   ========
你有使用过vue开发多语言项目吗？说说你的做法？   ========


在使用计算属性的时，函数名和data数据源中的数据可以同名吗？
    报错并被覆盖，因为Props、methods、data、computed、watch都是在initState函数中被初始化的。初始化顺序就是我上面给出的顺序，
    本质上这些都是要挂载到this上面的，你如果重名的话，后面出现的属性自然而然会覆盖之前挂载的属性了。


vue中data的属性可以和methods中的方法同名吗？为什么？
    在源码 initData 中  会取出 methods 中的方法进行判断，也就是 hasOwn(methods, key)
    如果此 key 值 在 methods 中存在，会有warn 警告哦****
    简言之 在初始化数据中会取出 methods 中的方法进行判断，若重复会进行警告。


怎么给vue定义全局的方法？

    1.注册到Vue 原型上。
    2.Vue.mixin()
    3.


怎么解决vue打包后静态资源图片失效的问题？
    保证 静态资源 在 src 下， 更改public 路径




怎么解决vue动态设置img的src不生效的问题？
    因为动态添加src被当做静态资源处理了，没有进行编译，所以要加上require。
    它把动态变量当成路径了，  用 require 加载即可。
    <!-- <img :src="require('@/assets/images/xxx.png')"/> -->

使用vue后怎么针对搜索引擎做SEO优化？
    SSR
    NUXT
    用vueMetaInfo与prerenderSpaPlugin进行预渲染
    https://segmentfault.com/a/1190000019623624



跟keep-alive有关的生命周期是哪些？描述下这些生命周期
如果现在让你从vue/react/angularjs三个中选择一个，你会选哪个？说说你的理由

你知道vue2.0兼容IE哪个版本以上吗？
    IE-9 及以上


使用vue开发一个todo小应用，谈下你的思路
你有看过vue推荐的风格指南吗？列举出你知道的几条
你是从vue哪个版本开始用的？你知道1.x和2.x有什么区别吗？
你知道vue中key的原理吗？说说你对它的理解



vue中怎么重置data？
    this.$data  ===> 当前的data值
    this.$options.data()  ===> data的初始值
    Object.assign(this.$data, this.$options.data())




vue渲染模板时怎么保留模板中的HTML注释呢？
    template 旁加 comments

Vue.observable你有了解过吗？说说看



你知道style加scoped属性的用途和原理吗？
    用途：加了 scoped 的样式只对当前组件有效，不会污染全局样式。防止全局同名CSS污染
    原理：Vue 会在元素标签加上 [data-v-xxx] 属性，然后在 CSS 选择器加上对应属性选择器，以完成类似作用域的效果。


你期待vue3.0有什么功能或者改进的地方？

vue边界情况有哪些？


如何在子组件中访问父组件的实例？
    1.this.$emit('name', data);
    2.this.$parent.event
    3.通过 props  直接把方法传进来。

watch的属性用箭头函数定义结果会怎么样？ 在vue项目中如果methods的方法用箭头函数定义结果会怎么样？
    1.箭头函数绑定了父级作用域的上下文，所以this不会指向VUE实例。因此会报错undefined



在vue项目中如何配置favicon？ ========


你有使用过babel-polyfill模块吗？主要是用来做什么的？
    更好的辅助Babel 兼容ES6。Babel 主要是转换新JS（ES6）的句法，而对于一些新增 的API（Set, Map， Proxy）或者 全局方法（Array.form()都不会转码。

说说你对vue的错误处理的了解？
    1.可以通过 Vue.config.errorHandler = (err, vm, info ) =>{}      在父组件中处理子组件的错误
    2.可以通过 Vue.config.warnHandler = (err, vm, trace ) =>{}      trace 组件树
    3.可以通过 renderError(h, err) {
        return h("pre", { style: { color: "red" } }, err.stack);
        }    
    4.在组件中使用 errorCaptured(err, vm, info) {
        console.log(`cat EC: ${err.toString()}\ninfo: ${info}`);
        return false;
      }         当捕获一个来自子孙组件的错误时被调用。
    5.window.onerror  全局捕获

    作者：Fundebug
    链接：http://www.imooc.com/article/288017?block_id=tuijian_wz
    来源：慕课网


在vue事件中传入$event，使用e.target和e.currentTarget有什么区别？
    e.target 指向事件发生时的元素，
    e.currentTarget 指向事件所绑定的元素。

在.vue文件中style是必须的吗？那script是必须的吗？为什么？
vue怎么实现强制刷新组件？
    1.  在组件内  ===》 this.$forceUpdate();
    2. 刷新某个子组件
        2.1动态改变 子组件的  key 值（当组件的key 值变更时，会自动的重新渲染）。  ：key="value"  value++
        2.2 v-if
    


vue自定义事件中父组件怎么接收子组件的多个参数？
    arguments   
    //子组件
        this.$emit('teest', this.params1,this.params2,this.params3,);
    //父组件
        @test=test(arguments, fatherDefineParams)

实际工作中，你总结的vue最佳实践有哪些？


vue给组件绑定自定义事件无效怎么解决？
    1.在自定义组件中绑定原生事件 ，需添加 .native ； eg:    @click.native=function(){}
    2.通过   this.$emit('name',value) 方法。



vue的属性名称与method的方法名称一样时会发生什么问题？
    会报错，在 初始化的时候 会进行检查
    键名优先级：props > data > methods



vue变量名如果以_、$开头的属性会发生什么问题？怎么访问到它们的值？
    会报错，eslint也会提示。
    可以使用 $data.xx 或者 _data.xx 访问

vue使用v-for遍历对象时，是按什么顺序遍历的？如何保证顺序？
vue如果想扩展某个现有的组件时，怎么做呢？
说下$attrs和$listeners的使用场景
分析下vue项目本地开发完成后部署到服务器后报404是什么原因呢？


v-once的使用场景有哪些？
    v-once 只渲染元素和组件一次，其后 不再随着数据的改变而重新渲染。



说说你对vue的表单修饰符.lazy的理解
    .lazy   一般默认 v-model  在 @input 事件时就更新数据，而加上了 .lazy 就会在 失焦事件或回车时 更新。
    .number  会将数据的 数据类型转化为 number。(仅是 data里面的数据类型， dom节点里面的数据还是 字符串)
    .trim    自动过滤输入的首尾空格

vue为什么要求组件模板只能有一个根元素？
    1.每个.vue 文件都代表着 一个  vue实例，它需要一个唯一的入口进行渲染，生成v-dom，若有多个入口则无法解析。
    2.当前（2.X）的diff算法/v-dom 是基于  在父级v-dom中，每个子组件都代表着一个单独的v-node, 因此 不支持多个节点。f发

EventBus注册在全局上时，路由切换时会重复触发事件，如何解决呢？
怎么修改vue打包后生成文件路径？
你有使用做过vue与原生app交互吗？说说vue与ap交互的方法
使用vue写一个tab切换
vue中什么是递归组件？举个例子说明下？


怎么访问到子组件的实例或者子元素？、
    this.$refs.xxx 
    this.$children

在子组件中怎么访问到父组件的实例？
    this.$parent.xx
    this.$emit('data',  event)
    prop

在组件中怎么访问到根实例？
    $root

说说你对Object.defineProperty的理解
vue组件里写的原生addEventListeners监听事件，要手动去销毁吗？为什么？


vue组件里的定时器要怎么销毁？
    const timer = setInterval(()=>{
        console.log(11)
    });
    this.$once('hook:beforeDestory',  ()=>{
        clearInterval(timer)
    })


vue组件会在什么时候下被销毁？
    1.v-if
    2.改变key值
    3.页面关闭、路由跳转     ------destoryed



使用vue渲染大量数据时应该怎么优化？说下你的思路！
    如果一次性传入大量数据
        1.按需加载局部数据，通过  虚拟列表 和 无限下拉刷新 实现；
        2.纯数据展示 -可采用 Object.freeze() 冻结对象。
        3.分页处理。
    只是分段加载 
        1.按需加载组件，异步渲染组件
        2.使用vue的v-if 最多显示上中（可视区域）下三屏 避免出现大量的dom节点


在vue中使用this应该注意哪些问题？
    1.在vue中通过  axios 网络请求时,会遇上 this指向undefined，而不指向  vue 的问题 。
        1.1 通过 箭头函数 解决。
            1.1.1 示例：        catch((error)=> {
                                    console.log(this); //箭头函数"=>"使this指向vue
                                });
        1.2 通过  hack 写法。
            1.2.1   ；示例：        let _this = this;
                                   this.$axios.post("……")
                                       .then(function(response){
                                           console.log(_this); //这里 _this 指向 vue
                                       })
                                   })
    2.生命周期的钩子函数不能使用箭头函数，否者this不能指向vue实例



你有使用过JSX吗？说说你对JSX的理解
说说组件的命名规范
怎么配置使vue2.0+支持TypeScript写法？


<template></template>有什么用？

    当做一个不可见的包裹元素，减少不必要的DOM元素，整个结构会更加清晰。
    包裹嵌套其它元素，使元素具有区域性，自身具有三个特点：
        *隐藏性：不会显示在页面中
        *任意性：可以写在页面的任意地方
        *无效性： 没有一个根元素包裹，任何HTML内容都是无效的


vue的is这个特性你有用过吗？主要用在哪些方面？
    1.动态切换组件
    2.突破html模板的限制。（eg:    ul  和  li)


vue的:class和:style有几种表示方式？
你了解什么是函数式组件吗？
vue怎么改变插入模板的分隔符？
组件中写name选项有什么作用？
说说你对provide和inject的理解
开发过程中有使用过devtools吗？
说说你对slot的理解有多少？slot使用场景有哪些？
你有使用过动态组件吗？说说你对它的理解


prop验证的type类型有哪几种？

    8种， String,  Number, Boolean, Function, Object, Array, Date, Symbol

    props:{
        title:String,
        likes: Number,
        isPublished: Boolean,
        commentIds: Array,
        author: Object,
        callback: Function,
        contactsPromise: Promise,
        propF: {
            type: String,
            validator: function (t) {
                // 这个值必须匹配下列字符串中的一个
                return t === 'fade' || t === 'slide'
            },
            defalut:'slide'
        },
        propE: {
            type: Object,
            // 对象或数组且一定会从一个工厂函数返回默认值
            default: function () {
                return { message: 'hello' }
            }
        },
    }


prop是怎么做验证的？可以设置默认值吗？
    通过 validator 进行自定义校验， 若不通过则会在console中进行提示。
    通过default 属性设置默认值， 基础数据类型 就直接赋值就行，而对象或者数组 需要通过工厂函数返回默认值。


怎么缓存当前打开的路由组件，缓存后想更新当前组件怎么办呢？
说说你对vue组件的设计原则的理解
你了解vue的diff算法吗？

vue如何优化首页的加载速度？
    1.减少请求次数，
        1.1 按需加载，（1）单页应用下的按照路由的需要加载 （2）缓存
        1.2 css雪碧图
        1.3 cdn托管
        1.4 延迟加载
    2.减少量
        2.1 精简代码（tree-sharking）
        2.2 路由的懒加载
        2.3 压缩 1）webpack 压缩UglifyJsPlugin；（2）gzip压缩 (3)图片压缩、JPG优化
        2.4 缓存 http 代码，浏览器的强缓存和协商缓存 
        2.5.第三方组件---第三方组件作为外部依赖使用，会被打包进业务代码（webpack提供的externals）。
        2.6.按需加载 --- （1）第三方库和工具的按需加载，如echarts （2）选择更优的工具 day.js代替moment （3）可用代码拆分（Code-splitting）只传送用户需要的代码
    3.减少内存的消耗
        3.1 减少全局变量；
        3.2.减少全局组件；
        3.3.减少dom操作， 减少DOM访问.
    4.webpack
        4.1 遇到webpack打包性能问题，先去npm run build --report，然后根据分析结果来做相应的优化，谁占体积大就干谁.
        4.2 webpack提供的externals（忽略打包的第三方库）可以配合外部资源CDN轻松大幅度减少打包体积，尤其对于echarts、jQuery、lodash这种库来说


强缓存和协商缓存
    浏览器 缓存分为 强缓存和协商缓存；
        强缓存：在第一次访问服务器拿到数据后，在过期时间内不会重复请求。
                在缓存期内，会直接采用本地缓存数据不请求数据，资源状态码为  200  ，资源的size为 from memory 或者  from disk.
              如何判断缓存是否过期？ 
                http1.0 expires 当发起的请求超过了 expires  ，则重新请求。
                http1.1 Cache-Control 字段： private：客户端可以缓存；public：客户端和代理服务器均可缓存；
                                            max-age=xxx：缓存的资源将在 xxx 秒后过期；no-cache：需要使用协商缓存来验证是否过期；
                                            no-store：不可缓存
        
        协商缓存： 协商缓存与强制缓存的不同之处在于，协商缓存每次读取数据时都需要跟服务器通信，并且会增加缓存标识。
                当第二次请求时 会先把缓存标识发给服务器，服务器拿到标识后 先进行匹配  若能匹配，则 从本地缓存中拿数据 返回，资源的状态码为 304；
                若不匹配，则说明资源有更新，服务器将最新的资源和缓存标识返回来。
                http1.0   last-modified If-Modified-Since
                http1.1   服务器通过 Etag 来设置响应头缓存标识。 


vue打包成最终的文件有哪些？



ajax、axios、fetch这三都有什么区别？
    1.ajax 封装了原生的 XHR，发送请求。多个请求之间如果有先后关系的话，就 容易陷入回调地狱。
    2.axios 基于XHR封装的Promise实现版本，与ajax的区别是从node.js 创建请求等
    3.fench 基于es6中的Promise对象设计的，是原生JS，没有使用XHR。（使用方便，但兼容性相对较差，且不能默认带cookie,也不能abort）



vue能监听到数组变化的方法有哪些？为什么这些方法能监听到呢？
       七种： splice/
            /push/pop
            /shift/ unshift
            /sort/reverse

        Vue 将上面这些数组方法进行了重写，
        重写方法在实现时除了将数组方法名对应的原始方法调用一遍并将执行结果返回外，还通过执行ob.dep.notify()  (相当于是挂了个watcher)将当前数组的变更通知给其订阅者，这样当使用重写后方法改变数组后，数组订阅者会将这边变化更新到页面中。


vue中是如何使用event对象的？
vue首页白屏是什么问题引起的？如何解决呢？
说说你对单向数据流和双向数据流的理解
移动端ui你用的是哪个ui库？有遇到过什么问题吗？
你知道nextTick的原理吗？
说说你对v-clock和v-pre指令的理解
写出你知道的表单修饰符和事件修饰符
说说你对proxy的理解
你有自己用vue写过UI组件库吗？
用vue怎么实现一个换肤的功能？
有在vue中使用过echarts吗？踩过哪些坑？如何解决的？
如果让你教一个2-3年经验前端经验的同事使用vue，你该怎么教？
vue性能的优化的方法有哪些？
SSR解决了什么问题？有做过SSR吗？你是怎么做的？
说说你觉得认为的vue开发规范有哪些？
vue部署上线前需要做哪些准备工作？
vue过渡动画实现的方式有哪些？
vue在created和mounted这两个生命周期中请求数据有什么区别呢？
vue父子组件双向绑定的方法有哪些？
vue怎么获取DOM节点？
vue项目有做过单元测试吗？
vue项目有使用过npm run build --report吗？
如何解决vue打包vendor过大的问题？
webpack打包vue速度太慢怎么办？
vue在开发过程中要同时跟N个不同的后端人员联调接口（请求的url不一样）时你该怎么办？
vue要做权限管理该怎么做？如果控制到按钮级别的权限怎么做？
说下你的vue项目的目录结构，如果是大型项目你该怎么划分结构和划分组件呢？
在移动端使用vue，你觉得最佳实践有哪些？
你们项目为什么会选vue而不选择其它的框架呢？
对于即将到来的vue3.0特性你有什么了解的吗？
vue开发过程中你有使用什么辅助工具吗？
vue和微信小程序写法上有什么区别？
怎么缓存当前的组件？缓存后怎么更新？
你了解什么是高阶组件吗？可否举个例子说明下？
为什么我们写组件的时候可以写在.vue里呢？可以是别的文件名后缀吗？
vue-loader是什么？它有什么作用？
说说你对vue的extend（构造器）的理解，它主要是用来做什么的？
如果将axios异步请求同步化处理？
怎么捕获组件vue的错误信息？
为什么vue使用异步更新组件？

写出多种定义组件模板的方法
SPA单页面的实现方式有哪些？
说说你对SPA单页面的理解，它的优缺点分别是什么？
说说你都用vue做过哪些类型的项目？
在vue项目中如何引入第三方库（比如jQuery）？有哪些方法可以做到？
使用vue手写一个过滤器
你有使用过render函数吗？有什么好处？
写出你常用的指令有哪些？
手写一个自定义指令及写出如何调用
组件进来请求接口时你是放在哪个生命周期？为什么？
你有用过事件总线(EventBus)吗？说说你的理解
说说vue的优缺点分别是什么？



DOM渲染在哪个周期中就已经完成了？
    mounted中
第一次加载页面时会触发哪几个钩子？
    beforeCreate created beforeMounte mounted
vue生命周期总共有几个阶段？
    1.8个 beforeCreate created beforeMounte mounted beforeUpdate updated beforeDestroy  destroyed
vue生命周期的作用是什么？
    它的生命周期中有多个事件钩子，让我们在控制整个Vue实例的过程时更容易形成好的逻辑。


如何引入scss？引入后如何使用？
    npm install  -D node-sass sass-loader
    style样式标签上添加lang=”scss”，


使用vue开发过程你是怎么做接口管理的？
    axios拦截





vue和angular有什么区别呢？
为何官方推荐使用axios而不用vue-resource？
你了解axios的原理吗？有看过它的源码吗？


你有封装过axios吗？主要是封装哪方面的？     +++++++++
1.请求拦截
    设置请求头/超时时间/， 参数。
2.响应拦截
    错误处理--验证token是否过期
    取消重复请求（节流）    axios.CancelToken.source().token    https://blog.csdn.net/zimeng303/article/details/112253644
    


如何中断axios的请求？
axios是什么？怎样使用它？怎么解决跨域的问题？
说说你对vue的template编译的理解？
v-on可以绑定多个方法吗？
vue常用的修饰符有哪些？列举并说明
你认为vue的核心是什么？
v-model是什么？有什么用呢？
说说你对vue的mixin的理解，有什么应用场景？
SPA首屏加载速度慢的怎么解决？
删除数组用delete和Vue.delete有什么区别？
动态给vue的data添加一个新的属性时会发生什么？怎样解决？
组件和插件有什么区别？
说说你使用vue过程中遇到的问题（坑）有哪些，你是怎么解决的？
说说你对选项el,template,render的理解
vue实例挂载的过程是什么？
vue在组件中引入插件的方法有哪些？
v-if和v-for的优先级是什么？如果这两个同时出现时，那应该怎么优化才能得到更好的性能？
分别说说vue能监听到数组或对象变化的场景，还有哪些场景是监听不到的？无法监听时有什么解决方案？
$nextTick有什么作用？
为什么data属性必须声明为返回一个初始数据对应的函数呢？
怎么在watch监听开始之后立即被调用？
watch怎么深度监听对象变化？
watch和计算属性有什么区别？
vue如何监听键盘事件？
v-for循环中key有什么作用？
怎么在vue中使用插件？
你有写过自定义组件吗？


说说你对keep-alive的理解是什么？
    1.包裹动态组件，缓存不活动的组件实例。
    2.常用包裹内容
        2.1 component is属性 ---动态组件
        2.2 v-if
        2.3 包裹路由    <keep-alive>
                            <router-view/>
                        </keep-alive>
    3.精准匹配某组件
        3.1 include/exclude  include 匹配上了就缓存，支持字符串/正则/数组
        3.2 v-if +  路由元信息  <keep-alive>
                                    <router-view v-if="$route.meta.xxx">
                                </keep-alive>

路由切换，页面不更新的实用方法?
    1.加key


怎么使css样式只在当前组件中生效？
你有看过vue的源码吗？如果有那就说说看

你有写过自定义指令吗？自定义指令的生命周期（钩子函数）有哪些？
    1.bind
    2.inserted
    3.update
    4.componentUpdated
    5.unbind

    Vue.directive('my', {
        bind(el){

        },

    })


v-show和v-if有什么区别？使用场景分别是什么？
说说你对MVC、MVP、MVVM模式的理解

                            
说下你对指令的理解？
    需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。


请描述下vue的生命周期是什么？
8+2  ===> beforeCreate   created  beforeMounte Mounted beforeUpdate  updated  beforeDestory destoraged   + activated deactivated 


vue组件之间的通信都有哪些？
    1.父子之间
        1.1 props, 
        1.2 ref,
        1.3 $parent/$children,
            $parent/$children   ---谨慎使用---》$children的顺序不稳定，且不是响应式的。

    2.兄弟组件传值
        Bus  (Bus.$emit('xx',  data)  ===>  Bus.$on('xx', (data)=>{ console.log(data) }))   
             移除监听===》Bus.$off('xx',  data)
        Vuex
    3.跨级通信
        Bus， Vuex, provide/inject, $attrs/$listeners
    4.storage ===> sessionStorage/localStorage
        
    vue中8种组件通信方式, 值得收藏!
    https://juejin.cn/post/6844903887162310669





     
        
什么是 重绘/回流？
回流： 当render  tree 中元素的结构，布局，大小 ，隐藏状况发生改变而需要重新构建的状况就称为回流。
重绘： 当 rendertree 中元素需要更新属性，而这些属性只影响风格/外观，不个影响布局的，就称为 重绘。
回流一定导致重绘。


什么是虚拟DOM？
    用一个JS对象来表示或模拟一个真实DOM的结构。

为啥要虚拟dom?
    因为用JS修改DOM效率低，每次修改后，它的子项都会经过重绘或回流，而重绘或回流一多就很影响性能。但是JS运行速度快，虚拟DoM是放在JS和 html中间的一层，在数据变动后，会比较新旧节点的差异，有针对性的将差异部分真正的渲染到页面上，从而减少dom操作，最终达到性能优化的效果。

如何实现一个虚拟DOM？说说你的思路
    //创建 v-dom的 构造函数
    class Element {
        constructor(type, props, children){
            this.type = type;
            this.props = props;
            this.children = children;
        }
    }
    //实例化
    function createElement(type, props, children){
        return new Element(type, props, children);
    }

    <!-- const createElement = (type, props, children) => new Element(type, props, children); -->
    上面就基本描述了DOM的树形结构 

    // 创建单个真实dom元素
    function createNode(node){
        let el = document.createElement(node.type);
        for(key in node.props){
            if(key == 'value'){
                if(node.type.toUpperCase()=='INPUT' || node.type.toUpperCase()=='TEXTAREA'){
                    el.value = node.props[key];
                }
            }else{
                el.setAttribute(key, node.props[key])
            }
        }

        return el;
    }

    //创建dom树
    function createDom(node){
        let root = createNode(node);
        if(node.children && node.children.length>0){
            node.children.forEach(element => {
                if(element instanceof Element){
                    root.appendChild(createDom(element))
                }else{
                    root.appendChild( document.createTextNode(element) );
                }
            })
        }
        return root;
    }

    应用：
    let vDom = createElement("ul", {class: "dawd"}, [
    	createElement("li", {class: "dawd"}, ["1"]),
    	createElement("li", {class: "dawd"}, ["2"]),
    	createElement("li", {class: "dawd"}, ["3"])
    ]);
    let dom = createDom(vDom);
    document.getElementsByTagName("body")[0].appendChild(dom);

    参考：
    https://juejin.cn/post/6844903858531991559


什么是双向绑定？原理是什么？
Vue 主要通过数据劫持，配合 发布-订阅者模式，通过defineProperty() 劫持各个属性的setter 和getter,在数据变动时，发布消息给订阅者，触发响应回调。
  


vue和react有什么不同？使用场景是什么？

说说vue的优缺点
    1.优点： 
        1.1 组件化开发 ====》 提高开发效率，方便复用， 提升整个项目的可维护性，便于协同开发 
        1.2 V-dom


有使用过vue吗？说说你对vue的理解


vuex

你有写过vuex中store的插件吗？
你有使用过vuex的module吗？主要是在什么场景下使用？
vuex中actions和mutations有什么区别？
vuex使用actions时不支持多参数传递怎么办？

你觉得vuex有什么优缺点？
    1.优点
        1.1 方便非父子组件通信
        1.2 方便共用数据，减少请求
    2.缺点
        刷新后，数据还原。 ===》通过 sessionStorage /replaceState /removeItem    或者  vuex-persistedstate  


你觉得要是不用vuex的话会带来哪些问题？
vuex怎么知道state是通过mutation修改还是外部直接修改的？
请求数据是写在组件的methods中还是在vuex的action中？
怎么监听vuex数据的变化？
vuex的action和mutation的特性是什么？有什么区别？


页面刷新后vuex的state数据丢失怎么解决？
    1/通过监听刷新事件（beforeUnload）,先通过sessionStorage 保存state数据，
      然后在created中 通过this.$store.replaceState() 方法设置相应数据，并清除sessionStorage中保存的数据。
    2/数据持久化vuex-persistedstate    ====> 默认 localStorage



vuex的state、getter、mutation、action、module特性分别是什么？
vuex的store有几个属性值？分别讲讲它们的作用是什么？
你理解的vuex是什么呢？哪些场景会用到？不用会有问题吗？有哪些特性？
使用vuex的优势是什么？
有用过vuex吗？它主要解决的是什么问题？推荐在哪些场景用？

作者：浪子神剑
链接：https://juejin.cn/post/6844903876231954446
来源：掘金
著作权归作者所有。商业转载请联系作者获得授权，非商业转载请注明出处。




发布项目（部署构建）步骤：
本地执行 npm run build 构建项目，压缩编译好的资源文件
将压缩包丢到远程服务器
ssh到远程服务器，解压压缩包
配置nginx



1.你知道vue的模板语法用的是哪个web模板引擎的吗？说说你对这模板引擎的理解.

mustache，主要是使用{{}}进行数据渲染。
2.你知道v-model的原理吗？那双向绑定的原理呢？

    v-model是一个语法糖，真正实现双向绑定还是依靠v-bind：绑定响应式数据。以及触发input事件并传递数据（核心和重点） =====》 事件监听和属性绑定

    双向绑定的原理：
        1.通过Observer把数据劫持（Object.defineProperty()），加入到订阅器（Dep）,订阅器收集订阅者（watch），视图通过编译（Compile）
            解析指令（Directive）等一系列操作收集给订阅者，最后通过触发数据变化update通知所有的订阅者完成数据驱动。
        2.直白的理解为：Object.defineProperty()重新定义了set和get方法，修改触发set方法赋值。获取触发get方法取值，并通过数据劫持发布信息。

        其他： Observer ---数据的观察者
              watcher  ---数据的订阅者
              Dep      ---Observer 和 Watcher  的纽带，当数据变化时由Observer察觉到，通过 Dep.notify() 通知 watcher, 然后由它更新视图。


        Vue数据双向绑定原理是什么？
        面试官：说下Vue数据双向绑定原理是什么？

        ME: 固定回答：

            Vue的数据双向绑定原理是数据劫持，结合发布订阅者模式，通过Object.defineProperty()来劫持各个属性的setter,getter属性，当数据变化时发布消息给订阅者，触发对应的回调函数。

        面试官: 可以具体说下吗？详细一点？

        ME: 这怎么答？其他没看呀？再想想，好像是。。。

        需要Observe的数据对象进行递归遍历，包括子属性对象的属性，都加上setter,与getter,这样的话这个对象的属性赋值，就会触发setter,就能监听到数据变化了
        Compile解析模板指令，将模板中的变量替换成数据，然后初始化页面视图，并将每个指令对应的节点绑定新函数，添加监听数据的订阅者，一旦数据又变动，收到通知，更新视图
        Watcher就是那个订阅者，主要就是连接Observer与Compile之间的桥梁：  
                    · 在自身实例话时往属性订阅器里面添加自己

                    · 自身有一个Update（）的方法

                    · 待属性变动dep.notice()通知时，能调用自身的update()方法，并触发Compile中绑定的回调






3.你知道vue中key的原理吗？说说你对它的理解

便于diff算法的更新，key的唯一性，能让diff算法更快的找到需要更新的dom节点。
4.Vue.Observable你有了解过吗？

vue2.6发布的一个新的api，可以处理简单的跨组件共享数据状态的问题。
精简版的vuex。
5.你知道style加scoped属性的用途和原理吗？

1.用途：防止全局同名css污染。
2.原理：在标签上添加v-data-something属性，再在选择器加上对应[v-data-something],即css带属性选择器，以此完成类似作用域的选择方式。
6.$nextTick的作用

复制代码

// 官方文档：下次DOM更新循环结束执行延迟回调，在修改数据之后立刻调用这个方法，就会获取更新后的DOM。

//什么时候用到Vue.$nextTick();

//1.created初始化状态的时候没有挂载dom元素，所以此时需要操作dom元素就必须使用$nextTick();
//2.mounted不会承诺所有的子组件也都一起被挂载，如果你希望等到整个视图都渲染完毕，可以用$nextTick()替换mounted。

mounted:function(){
   this.$nextTick(()=>{
       
   })
}



2020-05-17 美团W

NEW操作符到底干了什么？
    1.创建一个空对象； let obj = Object.create(null);
    2.设置原型链，让新对象的原型属性（__proto__）指向函数的原型链（prototype）；    obj._proto_ = Fun.prototype;
    3.让fn的this指向obj，并执行fn的函数体。  改变this指向（让构造函数的this指向 新建的对象），并执行函数； let result = Fun.call(obj, arguments);
    4.判断fn的返回值类型，如果是值类型，返回obj。如果是引用类型，就返回这个引用类型的对象。
        //return result instanceof object ? result : obj;


对Vue.use()的理解？
    Vue.use(plugins：object || function, args)的第一个参数是对象或者方法，如果是对象，就执行对象中的install方法，否则就直接执行传入方法。
    1.是一个全局注册组件或插件的方法。

    2.每次注册前，都会判断一下这个组件或者插件(plugins)是否注册过，如果注册过，就不会再次注册了。
    然后将我们传入的非组件参数整理成数组，再将Vue对象添加到这个数组的起始位置args.unshift(this),

    plugin参数的限制为 对象和方法 两种类型， 如果是对象，就直接传入上面的参数数组  执行对象的install方法；否则就直接带上参数执行方法。
    之后就将此plugin 添加到插件数组中，标识着已经注册。
    最后返回  Vue 对象。

    
本地缓存的理解
    1.本地存储包括cookie， sessionStorage，localStorage三种
    2.sessionStorage和localStorage两个只是本地存储，不能与浏览器进行通信；
    　　cookie 的内存比较小，大概4kb，sessionStorage和localStorage大概5M；受同源策略影响不能跨域。

    3.能提高访问服务端的效率，但是安全性较差！
    4.cookie 它的主要用途有保存登录信息。


跨域
JSONP 的工作原理是什么？
    利用<script>标签没有跨域的限制来达到与第三方通讯的目的。
    本站脚本创建一个<script>元素，地址指向第三方的API网址，并提供一个回调函数来接收数据（函数名可约定，或通过地址参数传递）。     第三方产生的响应为json数据的包装（故称之为jsonp，即json padding），形如：     callback({"name":"hax","gender":"Male"})     这样浏览器会调用callback函数，并传递解析后json对象作为参数。本站脚本可在callback函数里处理所传入的数据。

跨域资源共享（cors）