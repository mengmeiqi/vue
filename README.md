# vue
vue֪ʶ��

### 1.��վ��
    https://cn.vuejs.org/
    Github��https://github.com/vuejs/vue
### 2.�����µ�Vue
      var vm = new Vue();
      var vm = new Vue({
            el:'',//elements����дһ��ѡ��������ѡ�����ķ�Χ����������
            data:{},//����дһЩ����
            computed:{}//��������
            methods:{}//����дһЩ����
      });
### 3.��ֵ{{}}:˫�����ŵ��ı���ֵ
      ʾ��:Hello world!
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
### 4.ָ��
      (1)v-if v-else v-else-if v-show
      <div v-if="type == 'A'">��ӭ��:Ψ��</div>
      <div v-else-if="type == 'B'">���¼</div>
      <div v-else>C</div>
      v-if��v-show������
            ��v-show:�ı���display��ֵ������false��Ϊdisplay:none
            �ڶ��߶��Ƿ��ز���ֵ
            ��v-if��dom�ṹ�У�v-show����dom�ṹ��
      (2)v-for
          <ul><li v-for="(school,index) in list" :key="index">
          {{school}}--{{index}}
          </li></ul>
      ��arr��������:
          sortArr:function(){
            return this.arr.sort(function(a,b){
                return a-b;
            });
          }
      (3)v-text,v-html
         �ٷ�ֹ������ˢ��ʱ����
         ��v-text�ı������v-html������ǩ
         ��v-html�а�ȫ������
      (4)v-on ��д��ʽ @
         A.������event
         B.���η���
         ��.stop:����event.stopPropagation()
         ��.prevent:����event.preventDefault()
         ��.once:ֻ����һ�λص�
         ��.enter:�س�������13
         <button @click.once = "add(1,$event)">��1</button>
         <div class="div1" @click='clickDiv1'>
            <div class="div2" @click.stop='clickDiv2'></div>
         </div>
      (5)v-model
        A.����
        ��<input> ��<select> ��<textarea>
        B.���η�
        ��.number ��.trim ��.lazy
        <label>�û��� <input type="text" v-model="username"></label>
        <label>�û��� <input type="text" v-model.lazy="username"></label>
        <label>�û��� <input type="number" v-model.number="username"></label>
        <label>�û��� <input type="text" v-model.trim="username"></label>
      (6)v-bind�� ����д��ʽ :
        ��̬�ذ�һ���������ԣ���һ�����prop�����ʽ
        <img :src="imgSrc" :alt="imgAlt">
        <div :class="clsName">div1</div>
        <div :class="{bb:isBb}">div2</div>
        <div :class="{aa: isAa, bb: isBb}">div3</div>
        <div :style="styleObj">div4</div>
        <div v-bind:class="[activeClass, errorClass]"></div>
        data: {
            imgSrc: 'https://cn.vuejs.org/images/logo.png',
            imgAlt: 'ͼƬ����ʧ����',
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
            �������Ԫ�غ�������Ԫ�صı�����̡�����������ʾԭʼ Mustache ��ǩ����������û��ָ��Ľڵ��ӿ���롣
            <div v-pre>{{msg}}</div> ���:{{msg}}  ���ñ�ǩ���廯
      (8)v-cloak
            ��Ⱦ����Ժ���ִ��
      (9)v-once
            ֻ��ȾԪ�غ����һ�Ρ�����������Ⱦ��Ԫ��/����������е��ӽڵ㽫����Ϊ��̬���ݲ�����������������Ż��������ܡ�
### 5.�Ƽ� MDN : https://developer.mozilla.org
### 6.forEach��filter����
            ���߶��Ǳ���ѭ����filter�з���ֵ��forEeachû�з���ֵ
### 7.��ָ����Ӻ�����
      (1)����(hook)��
            ������js��vue�������еģ�������windows����ģ�����һ����֮ǰ����һ����֮��Ҫ��ʲô�£��������ӡ��������Ҫ���أ��ڼ���֮ǰ���߼��سɹ�֮����һЩ��������ô����֮ǰ�ͼ��سɹ�֮��ͽ������ӡ�
      (2)������
            A.el:ָ�����󶨵�Ԫ�أ���������ֱ�Ӳ���DOM
            B.binding:һ�����󣬰�����������:
            ��name ��value ��oldValue
            ��expression ��arg ��modifiers
            C.vnode:Vue�������ɵ�����ڵ�
            D.oldVnode:��һ������ڵ㣬����update��componentUpdated�����п���
      (3)vue������dom
            vue��dom�����ϱ�jQuery���ܸߣ�vue��������ʵ����dom�ģ�vue�����ݲ�����vue�ڴ�����һ������dom���ѵ�ǰ��״̬����һ�ε�״̬���бȽϣ���������κ��ϴ�dom��ͬ�ĵط�ͬ������ʵdom�ϣ�������ˢ������dom������˵���ܻ���ߣ�vnode���ص�������dom�Ľڵ�

      (4)ָ��庯���ṩ�˼������Ӻ�����
            A.bind:ֻ����һ�Σ�ָ���һ�ΰ󶨵�Ԫ��ʱ���ã���������Ӻ������Զ���һ���ڰ�ʱִ��һ�εĳ�ʼ������
            B.inserted:����Ԫ�ز��븸�ڵ�ʱ����
            C.update:���������VNode����ʱ����
            D.componentUpdated:���������VNode�����ӵ�VNodeȫ������ʱ����
            E.unbind:ֻ����һ�Σ�������ʱ���ã�ָ����Ԫ�ؽ��ʱ����
### 8.�Զ���ָ��
            ���˺��Ĺ���Ĭ�����õ�ָ�� (v-model?��?v-show)��Vue Ҳ����ע���Զ���ָ�ע�⣬�� Vue2.0 �У����븴�úͳ������Ҫ��ʽ�������Ȼ�����е�����£�����Ȼ��Ҫ����ͨ DOM Ԫ�ؽ��еײ��������ʱ��ͻ��õ��Զ���ָ�
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
            ���ֶ����� �����������
             ʹ�û���Vue������������һ�������ࡱ��������һ���������ѡ��Ķ���������data����һ��������һ��������
            (templateģ�� һ���ַ���ģ����Ϊ Vue ʵ���ı�ʶʹ�á�ģ�彫���滻���ص�Ԫ�ء�����Ԫ�ص����ݶ��������ԣ�����ģ��������зַ���ۡ�)
                    (components��� ����������Ϊ�Զ����ǩ )
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
                components:{  //���
                    'my-component':authorExtend   //myComponent
                }
            });
            mount������vue�����Դ��ĺ���
            ��� Vue ʵ����ʵ����ʱû���յ� el ѡ��������ڡ�δ���ء�״̬��û�й����� DOM Ԫ�ء�����ʹ��vm.$mount()�ֶ��ع���һ��δ���ص�ʵ����

            var MyComponent = Vue.extend({
                template: '<div>Hello!</div>'
            });
            // ���������ص� #app (���滻 #app)
            new MyComponent().$mount('#app');
      (3)Vue.set
            Vue.js���治����ʹ�á�����[�±�]����ʾ,vue����ͨ���������������ֵ,������鲻�ܸı��±������
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
### 9.��������
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
      beforeCreat(){ //����ǰ
            console.log('beforeCreat');
      },
      created(){ //�������
            console.log('created');
      },
      beforeMount(){ //����ǰ
            console.log('beforeMount');
      },
      mounted(){ //������� ��Ⱦ��� �ڴ˽׶β�����ʵDOM
            console.log('mounted');
      },
      beforeUpdate(){ //����ǰ
            console.log('beforeUpdate');
      },
      Updated(){ //�������
            console.log('Updated');
      },
      beforeDestroy(){ //����ǰ
            console.log('beforeDestroy');
      },
      destroyed(){ //�������
            console.log('destroyed');
      }
      vm.$destroy();
      ��ȫ����һ��ʵ����������������ʵ�������ӣ��������ȫ��ָ��¼���������
### 10.template��ǩ��ռDOM�ṹ
      <template v-if="isShow">
      <h1>HHHHH</h1>
      <h2>HHHHH</h2>
      </template>
      data: {
            isShow: false
      }
### 11.���
      ��� (Component) �� Vue.js ��ǿ��Ĺ���֮һ�����������չ HTML Ԫ�أ���װ�����õĴ��롣�ڽϸ߲����ϣ�������Զ���Ԫ�أ� Vue.js �ı�����Ϊ��������⹦�� ��
      ע�� 	��props:[]
            �ڲ����д� - ��ȥ����ܣ���������ĸ��д
            ��data ��ֵ���ݸ� ����� v-bind
      (1)ȫ������;ֲ����
        ����ȫ�����
        Vue.component();
        Vue.component('weichuang',{ //ȫ�����
            template:`
            <div>
                <h1>{{abcd}}</h1>
                <div>DIVDIV</div>
            </div>
            `,
            props:['abcd']
        });
        �ֲ����
            new Vue({
                el: '#app',
                data: {
                    msg: '����һ���ֲ����',
                    imgSrc:'',
                    msg2: 'hello',
                    msg3: '����һ��ȫ�����'
                },
                components: {
                    myComponent: {
                        template: `<h1>{{aa}}--{{bb}}</h1>`,
                        props: ['aa', 'bb']
                    }
                }
            });
      (2)���Ƕ��
### 12..native���η�
      ��ʱ�����������ĳ������ĸ�Ԫ���ϼ���һ��ԭ���¼�������ʹ��v-on�����η�.native��
      <my-component v-on:click.native="doTheThing"></my-component>
### 13.:is �л����
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
      <slot> Ԫ�ؿ�����һ����������� name ����һ��������ηַ����ݡ�
      �����ۿ����в�ͬ�����֡�������۽�ƥ������Ƭ�����ж�Ӧ slot ���Ե�Ԫ�ء�
      <div id="app">
          <weichuang>
              <h1 slot='username'>����</h1>
              <span slot='age'>18</span>
          </weichuang>
          <weichuang>
              <span slot='username'>����</span>
          </weichuang>
      </div>
      <template id="temp">
          <div>
              <div>
                  ���֣�
                  <slot name='username'></slot>
              </div>
              <div>
                  ���䣺
                  <slot name='age'>����Ĭ��ֵ</slot>
              </div>
          </div>
      </template>
### 15.$emit()
      ������ǰʵ���ϵ��¼������Ӳ������ᴫ���������ص���
      <span class="dialog-title-close" @click="$emit('close')">[X]</span>
      <my-dialog v-show="showRegister" @close="showRegister=false">
### 16.computed��watch
      computed:�������Խ������뵽Vueʵ���С�����getter��setter��this �������Զ��ذ�ΪVueʵ�����������ԵĽ���ᱻ���棬������������Ӧʽ���Ա仯�Ż����¼��㡣
      {{firstName}} + {{lastName}} = {{fullName}
      var vm = new Vue({
          el:'#app',
          data:{
              firstName:'Hello',
              lastName:'word',
          },
          computed:{
              fullName:function(){  //fullName�����������������
                return this.firstName+''+this.lastName;
              }
          }
      });
      watch:һ�����󣬼�����Ҫ�۲�ı��ʽ��ֵ�Ƕ�Ӧ�ص�����

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
### 17.Vue��˫�����ݰ�ԭ����ʲô��
      ����ES5����� Object.defineProperty()��ͨ��һ�����󣬽��������֮��Ĺ�ϵ��Vue�������ͨ�����Vue�����data������ʵ�ֵ�Object.defineProperty(); ����������
      ��һ���������������ĸ�����
      �ڶ�����������⵱ǰ�����������һ������
      ����������������������getֵ��setֵ
### 18.����DOM���ڴ����棬��ʵDOM�����������
      diff�㷨:�ҵ�ǰ��״̬����һ��״̬����Щ�������ı��ˣ��ѱ��ı�Ķ�����ʾ����ʵDOM�ڵ���

