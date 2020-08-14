# vue 2.0
# 课前备
vue官网 vuejs.org
资料地址 http://github.com/DuYi-Edu/DuYi-VUE
下载插件 vue-devtools
翻墙插件：https://github.com/qin-ziqi/Chrome-SetupVPN-3.7.0
vs code插件 : Markdown Preview Enhanced
# 脚手架

# 指令
    v-pre 跳过本身和子元素的编译过程
    v-cloak 
    v-once 只渲染一次
    v-text 跟新内容或替换文本
    v-html 跟新元素的innerHTML
    v-if  条件渲染
    v-else 配套使用
    v-else-if 配套使用
    v-show 判断真假 切换display属性
    v-bind 解析参数 :缩写
    v-on 绑定事件 @缩写  .stop阻止冒泡 .prevent阻止默认 .capture事件捕获 .self函数是methods内注册的才触发 .once只触发一次 .passive告诉浏览器不会阻止事件默认行为，提升性能   还有按键修饰符，系统修饰符，鼠标修饰符
    v-for 循环渲染  key值唯一
    v-model 双向数据绑定 多用于输入框 获取输入内容  修饰符 .lazy让其变为使用change事件同步数据 .number将用户的输入值变为数值类型 .trim去掉首位空白
# 插值表达式：{{}}
不要三连在一起{}
# vue实例参数
    el 绑定元素 接下来一系列操作都会在其绑定元素进行
    computed 计算属性 给一个函数，然后计算结果 计算属性的getter和setter
    methods  方法   和计算属性一样执行方法 不同的是 每一次页面渲染 无论值是否改变方法都会重新执行一遍
    template 选项 以字符串形式传递一个html 会被用来替代el绑定的元素  不写在vue实例上用来定义组件
    components 定义要使用的组件 
# 组件 模块化开发 替换指定标签
    Vue.component 全局组件   局部组件：const 组件名{data(){return},template:``}

    prop注册组件内的参数 使用props注册数据才可以在组件上使用 也可以进行组件验证规定传递的数据类型或固定值 prop会自动传递给子元素

   -  <keep-alive>包裹動態組件時，會緩存不活動的組件實例，而不是銷毀它們。<keep-alive>是一個抽象組件：它自身不會渲染一個DOM元素，也不會出現在父組件鏈中。
    當組件在<keep-alive>內被切換，它的activated和deactivated這兩個生命週期鉤子函數將會被對應執行。
# 插槽  实现在组件内添加内容
    在组件内添加内容 使用插槽<slot></slot>
    添加name属性变为具名插槽
    使用v-slot指令来使用插槽
# Axios 基于promise的http库
请求
拦截
响应
# 路由 通过路由可以实现模块化单页面  路由默认hash模式
 安装npm install vue-router
 引入 import VueRouter from  'vue-router' 
 使用 Vue . use ( VueRouter ) 
 定义路由组件
 定义路由
 创建router实例然后传入routes配置
 最后挂载到根实例
 - routes配置：
    routes = [
        {
            path:路由地址，
            name；地址太长 取个别名方便使用，
            redirect:重定向 也可以是一个命名的路由(对象形式) 也可以是方法形式
            alias:别名 就是使url后面的名字是别名
            component:组件 可以导入，
            children:[
                {
                    定义子路由
                    参数跟上面一样
                    子路由路劲可以简写
                }
            ]
        }
    ]


- 路由两种使用方式：
1.响应式：<router-link :to="..."></router-link>  使用router-link创建a标签实现导航
2.编程式:
        this.$router.push(...) 参数可以是路劲字符串 也可以是对象{name:''}
        this.$router.replace(...)  跟router.push 很像，唯一的不同就是，它不會向history 添加新記錄，而是替換掉當前的history 記錄。
        $router.go(n) 這個方法的參數是一個整數，意思是在history 記錄中向前或者後退多少步，類似window.history.go(n)
        还有很多方法
- 动态路由
- 。。
# vuex 实现组件间数据共享
npm install vuex -- save
import Vuex from  'vuex' 
Vue . use ( Vuex ) 

state 存放要共享的数据  $state.state在别的组件上使用
getter 和计算属性一样的作用
mutation 更改state内的值  （没有通过mutation 利用getter可以更改的原因是没有开启严格模式）  严格模式是开发环境下使用的 strict:true 
active 类似于mutation 不同在于 action通过提交mutation间接的更改state内的数据 且action可以包含任意异步操作

module 将store分割成模块 每个模块都拥有自己的stare mutation action getter