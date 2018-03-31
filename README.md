# vue
vue知识点

### 1.网站：
    https://cn.vuejs.org/
    Github：https://github.com/vuejs/vue
### 2.创建新的Vue
      var vm = new Vue();
      var vm = new Vue({
            el:'',//elements里面写一个选择器，在选择器的范围里面起作用
            data:{},//里面写一些数据
            computed:{}//计算属性
            methods:{}//里面写一些方法
      });
### 3.插值{{}}:双大括号的文本插值
      示例:Hello world!
      <div id="app">{{msg}}</div>
      <script src="vue.js"></script>
      <script>
            var vm = new Vue({
                el:'#app',
                data:{
                msg:'hello world'
                }
            });
            console.log(vm);
      </script>
### 4.指令
      (1)v-if v-else v-else-if v-show
      <div v-if="type == 'A'">欢迎你:唯创</div>
      <div v-else-if="type == 'B'">请登录</div>
      <div v-else>C</div>
      v-if与v-show的区别：
            ①v-show:改变了display的值，若是false则为display:none
            ②二者都是返回布尔值
            ③v-if在dom结构中，v-show不在dom结构中
      (2)v-for
          <ul><li v-for="(school,index) in list" :key="index">
          {{school}}--{{index}}
          </li></ul>
      给arr数组排序:
          sortArr:function(){
            return this.arr.sort(function(a,b){
                return a-b;
            });
          }
      (3)v-text,v-html
         ①防止内容在刷新时候闪
         ②v-text文本输出，v-html解析标签
         ③v-html有安全性问题
      (4)v-on 简写方式 @
         A.参数：event
         B.修饰符：
         ①.stop:调用event.stopPropagation()
         ②.prevent:调用event.preventDefault()
         ③.once:只触发一次回调
         ④.enter:回车键代码13
         <button @click.once = "add(1,$event)">加1</button>
         <div class="div1" @click='clickDiv1'>
            <div class="div2" @click.stop='clickDiv2'></div>
         </div>
      (5)v-model
        A.限制
        ①<input> ②<select> ③<textarea>
        B.修饰符
        ①.number ②.trim ③.lazy
        <label>用户名 <input type="text" v-model="username"></label>
        <label>用户名 <input type="text" v-model.lazy="username"></label>
        <label>用户名 <input type="number" v-model.number="username"></label>
        <label>用户名 <input type="text" v-model.trim="username"></label>
      (6)v-bind绑定 ，简写方式 :
        动态地绑定一个或多个特性，或一个组件prop到表达式
        <img :src="imgSrc" :alt="imgAlt">
        <div :class="clsName">div1</div>
        <div :class="{bb:isBb}">div2</div>
        <div :class="{aa: isAa, bb: isBb}">div3</div>
        <div :style="styleObj">div4</div>
        <div v-bind:class="[activeClass, errorClass]"></div>
        data: {
            imgSrc: 'https://cn.vuejs.org/images/logo.png',
            imgAlt: '图片加载失败啦',
            clsName : 'aa',
            isAa: true,
            isBb: true,
            styleObj: {
                width: '200px',
                'background-color': '#ccc'//backgroundColor
            },
            activeClass: 'active',
            errorClass: 'text-danger'
        }
      (7)v-pre
            跳过这个元素和它的子元素的编译过程。可以用来显示原始 Mustache 标签。跳过大量没有指令的节点会加快编译。
            <div v-pre>{{msg}}</div> 结果:{{msg}}  不让标签语义化
      (8)v-cloak
            渲染完成以后再执行
      (9)v-once
            只渲染元素和组件一次。随后的重新渲染，元素/组件及其所有的子节点将被视为静态内容并跳过。这可以用于优化更新性能。
### 5.推荐 MDN : https://developer.mozilla.org
### 6.forEach和filter区别：
            二者都是遍历循环，filter有返回值，forEeach没有返回值
### 7.（指令）钩子函数：
      (1)钩子(hook)：
            并不是js或vue里面特有的，最早是windows提出的，在做一件事之前或者一件事之后要做什么事，叫做钩子。比如界面要加载，在加载之前或者加载成功之后做一些操作，那么加载之前和加载成功之后就叫做钩子。
      (2)参数：
            A.el:指令所绑定的元素，可以用来直接操作DOM
            B.binding:一个对象，包含以下属性:
            ①name ②value ③oldValue
            ④expression ⑤arg ⑥modifiers
            C.vnode:Vue编译生成的虚拟节点
            D.oldVnode:上一个虚拟节点，仅在update和componentUpdated钩子中可用
      (3)vue是虚拟dom
            vue在dom操作上比jQuery性能高，vue并不是真实操作dom的，vue是数据操作，vue内存里有一个虚拟dom，把当前的状态和上一次的状态进行比较，仅仅把这次和上次dom不同的地方同步到真实dom上，而不是刷新整个dom，所以说性能会更高，vnode返回的是虚拟dom的节点

      (4)指令定义函数提供了几个钩子函数：
            A.bind:只调用一次，指令第一次绑定到元素时调用，用这个钩子函数可以定义一个在绑定时执行一次的初始化动作
            B.inserted:被绑定元素插入父节点时调用
            C.update:所在组件的VNode更新时调用
            D.componentUpdated:所在组件的VNode及孩子的VNode全部更新时调用
            E.unbind:只调用一次，（销毁时调用）指令与元素解绑时调用
### 8.自定义指令
            除了核心功能默认内置的指令 (v-model?和?v-show)，Vue 也允许注册自定义指令。注意，在 Vue2.0 中，代码复用和抽象的主要形式是组件。然而，有的情况下，你仍然需要对普通 DOM 元素进行底层操作，这时候就会用到自定义指令。
      (1)Vue.directive
            <h1 v-weichuang="aa">Hello world!</h1>
            Vue.directive('weichuang',{
                bind:function(el,binding,vnode){
                    el.style.background = binding.value;
                },
                inserted:function(){
                    console.log('inserted');
                },
                update:function(){
                    console.log('update');
                },
                componentUpdated:function(){
                    console.log('componentUpdated');
                },
                unbind:function(){
                    console.log('unbind');
                }
            });
            var vm = new Vue({
                el:'#app',
                data:{
                    aa:'green',
                }
            });
      (2)Vue.extend
            ①手动挂载 ②用在组件中
             使用基础Vue构造器，创建一个“子类”。参数是一个包含组件选项的对象。在这里data不是一个对象，是一个函数。
            (template模板 一个字符串模板作为 Vue 实例的标识使用。模板将会替换挂载的元素。挂载元素的内容都将被忽略，除非模板的内容有分发插槽。)
                    (components组件 组件可以理解为自定义标签 )
            <div id="app">
                <div id="div1"></div>
                    <my-component></my-component>
                    <my-component></my-component>
            </div>
            var authorExtend = Vue.extend({
                template:'<p><a :href="authorUrl">{{authorName}}</a></p>',
                data:function(){
                    return {
                        authorUrl:'http://www.baidu.com',
                        authorName:'xiecheng'
                    };
                }
            });
            new authorExtend().$mount("#div1");
            new Vue({
                el:'#app',
                components:{  //组件
                    'my-component':authorExtend   //myComponent
                }
            });
            mount函数是vue里面自带的函数
            如果 Vue 实例在实例化时没有收到 el 选项，则它处于“未挂载”状态，没有关联的 DOM 元素。可以使用vm.$mount()手动地挂载一个未挂载的实例。

            var MyComponent = Vue.extend({
                template: '<div>Hello!</div>'
            });
            // 创建并挂载到 #app (会替换 #app)
            new MyComponent().$mount('#app');
      (3)Vue.set
            Vue.js里面不允许使用’数组[下标]’表示,vue不能通过索引设置数组的值,解决数组不能改变下标的问题
            var vm = new Vue({
                el:'#app',
                data:{
                    list:['a','b','c','d']
                },
                methods:{
                    change(){
                        Vue.set(this.list,1,'e');
                    }
                }
            });
### 9.生命周期
      var vm = new Vue({
            el:'#app',
            data:{
            msg:1,
            timer:null
      },
      methods:{
            change(){
                this.msg++;
            },
            destroy(){
                vm.$destroy();
            }
      },
      beforeCreat(){ //创建前
            console.log('beforeCreat');
      },
      created(){ //创建完成
            console.log('created');
      },
      beforeMount(){ //挂载前
            console.log('beforeMount');
      },
      mounted(){ //挂载完成 渲染完成 在此阶段操作真实DOM
            console.log('mounted');
      },
      beforeUpdate(){ //更新前
            console.log('beforeUpdate');
      },
      Updated(){ //更新完成
            console.log('Updated');
      },
      beforeDestroy(){ //销毁前
            console.log('beforeDestroy');
      },
      destroyed(){ //销毁完成
            console.log('destroyed');
      }
      vm.$destroy();
      完全销毁一个实例。清理它与其它实例的连接，解绑它的全部指令及事件监听器。
### 10.template标签不占DOM结构
      <template v-if="isShow">
      <h1>HHHHH</h1>
      <h2>HHHHH</h2>
      </template>
      data: {
            isShow: false
      }
### 11.组件
      组件 (Component) 是 Vue.js 最强大的功能之一。组件可以扩展 HTML 元素，封装可重用的代码。在较高层面上，组件是自定义元素， Vue.js 的编译器为它添加特殊功能 。
      注： 	①props:[]
            ②参数中带 - ，去掉横杠，后面首字母大写
            ③data 的值传递给 组件： v-bind
      (1)全局组件和局部组件
        定义全局组件
        Vue.component();
        Vue.component('weichuang',{ //全局组件
            template:`
            <div>
                <h1>{{abcd}}</h1>
                <div>DIVDIV</div>
            </div>
            `,
            props:['abcd']
        });
        局部组件
            new Vue({
                el: '#app',
                data: {
                    msg: '这是一个局部组件',
                    imgSrc:'',
                    msg2: 'hello',
                    msg3: '这是一个全局组件'
                },
                components: {
                    myComponent: {
                        template: `<h1>{{aa}}--{{bb}}</h1>`,
                        props: ['aa', 'bb']
                    }
                }
            });
      (2)组件嵌套
### 12..native修饰符
      有时候，你可能想在某个组件的根元素上监听一个原生事件。可以使用v-on的修饰符.native。
      <my-component v-on:click.native="doTheThing"></my-component>
### 13.:is 切换组件
      <div :is="whichComponent"></div>
      data:{
        whichComponent:'component1'
      },
      components:{
          component1:{
            template:'<h1>component1</h1>'
          },
          component2:{
            template:'<h1>component2</h1>'
          },
          component3:{
            template:'<h1>component3</h1>'
          }
      }
### 14.slot
      <slot> 元素可以用一个特殊的特性 name 来进一步配置如何分发内容。
      多个插槽可以有不同的名字。具名插槽将匹配内容片段中有对应 slot 特性的元素。
      <div id="app">
          <weichuang>
              <h1 slot='username'>张三</h1>
              <span slot='age'>18</span>
          </weichuang>
          <weichuang>
              <span slot='username'>李四</span>
          </weichuang>
      </div>
      <template id="temp">
          <div>
              <div>
                  名字：
                  <slot name='username'></slot>
              </div>
              <div>
                  年龄：
                  <slot name='age'>我是默认值</slot>
              </div>
          </div>
      </template>
### 15.$emit()
      触发当前实例上的事件。附加参数都会传给监听器回调。
      <span class="dialog-title-close" @click="$emit('close')">[X]</span>
      <my-dialog v-show="showRegister" @close="showRegister=false">
### 16.computed和watch
      computed:计算属性将被混入到Vue实例中。所有getter和setter的this 上下文自动地绑定为Vue实例。计算属性的结果会被缓存，除非依赖的响应式属性变化才会重新计算。
      {{firstName}} + {{lastName}} = {{fullName}
      var vm = new Vue({
          el:'#app',
          data:{
              firstName:'Hello',
              lastName:'word',
          },
          computed:{
              fullName:function(){  //fullName经过计算产生的属性
                return this.firstName+''+this.lastName;
              }
          }
      });
      watch:一个对象，键是需要观察的表达式，值是对应回调函数

      var vm = new Vue({
          el:'#app',
          data:{
              firstName:'Hello',
              lastName:'word',
              fullName:''
          },
          watch:{
              firstName:function(val){
                this.fullName = val + '' + this.lastName
              },
              lastName:function(val){
                this.fullName = this.firstName + '' + val
              }
          }
      });
### 17.Vue的双向数据绑定原理是什么？
      答：用ES5里面的 Object.defineProperty()，通过一个对象，建立起二者之间的关系，Vue里面就是通过监测Vue对象的data属性来实现的Object.defineProperty(); 访问器属性
      第一个参数：监听的哪个对象
      第二个参数：监测当前对象里面的哪一个属性
      第三个参数：对象，里面有get值和set值
### 18.虚拟DOM在内存里面，真实DOM在浏览器里面
      diff算法:找当前的状态和上一个状态，哪些东西被改变了，把被改变的东西显示在真实DOM节点上

