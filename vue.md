# 组件

## 封装原则

1、单一原则：负责单一的页面渲染

2、多重职责：负责多重职责，获取数据，复用逻辑，页面渲染等

3、明确接受参数：必选，非必选，参数尽量设置以_开头，避免变量重复

4、可扩展：需求变动能够及时调整，不影响之前代码

5、代码逻辑清晰

6、封装的组件必须具有高性能，低耦合的特性

7、组件具有单一职责：封装业务组件或者基础组件，如果不能给这个组件起一个有意义的名字，证明这个组件承担的职责可能不够单一，需要继续抽组件，直到它可以是一个独立的组件即可。


## 组件通信

（1）**props / $emit** **适用** **父子组件通信**

1、父子 props 之间形成了一个单向下行绑定：父级 prop 的更新会向下流动到子组件中，但是反过来则不行。

​	子组件向父组件传递: $emit绑定一个自定义事件, 当这个语句被执行时, 就会将参数arg传递给父组件,父组件通过v-on监听并接收参数。

（2）**ref** **与 $parent / $children** **适用** **父子组件通信**

ref：如果在普通的 DOM 元素上使用，引用指向的就是 DOM 元素；如果用在子组件上，引用指向组件实例，父组件通过调用子组件ref名获取数据或调用方法，并且获取的是实时数据。

$parent / $children：访问父 / 子实例

**（3****）EventBus** **（$emit / $on****）** **适用于** **父子、隔代、兄弟组件通信**

这种方法通过一个空的 Vue 实例作为中央事件总线（事件中心），用它来触发事件和监听事件，从而实现任何组件间的通信，包括父子、隔代、兄弟组件。

（4）**$attrs/$listeners** **适用于** **隔代组件通信**

$attrs：包含了父作用域中不被 prop 所识别 (且获取) 的特性绑定 ( class 和 style 除外 )。当一个组件没有声明任何 prop 时，这里会包含所有父作用域的绑定 ( class 和 style 除外 )，并且可以通过 v-bind="$attrs" 传入内部组件。通常配合 inheritAttrs 选项一起使用。

$listeners：包含了父作用域中的 (不含 .native 修饰器的) v-on 事件监听器。它可以通过 v-on="$listeners" 传入内部组件

（5）**provide / inject** **适用于** **隔代组件通信** **（父—>****孙** **跨多层）**

祖先组件中通过 provider 来提供变量，然后在子孙组件中通过 inject 来注入变量。 provide / inject API 主要解决了跨级组件间的通信问题，不过它的使用场景，主要是子组件获取上级组件的状态，跨级组件间建立了一种主动提供与依赖注入的关系。

（6）**Vuex** **适用于** **父子、隔代、兄弟组件通信**

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

# 路由

根据不同的url地址展现不同的页面。前端路由的核心，就在于 —— 改变视图的同时不会向后端发出请求。

1定义路由组件

2引入路由组件

3配置路由routes

4实例化路由router

5把路由挂载到vue实例上（new vue）

6使用<router-link>组件给标签添加导航

7使用<router-view>给组件定义出口

## 导航守卫

Vue Router 是 Vue.js 官方的路由管理器。它和 Vue.js 的核心深度集成，让构建单页面应用变得易如反掌。

vue-router 提供的导航守卫主要用来通过跳转或取消的方式守卫导航。

定义全局前置守卫，判断地址是否可以访问：用getroutes获取当前路由表中存在的路由，与目标路由的path去比较 看是否存在

## SPA单页面应用

单页Web应用（single page web application，SPA）

- 很多页面存在很多重复的代码，比如页面公共部分，页头页脚等，虽然可以写成模板避免重复，但是浏览器每次都会请求重复的资源，浪费了网络资源

- 一些公共的样式文件，js脚本文件也会被重复请求

  为了解决上面的一些问题，有经验的开发者提出了一种解决方案---SPA，即把页面内容和逻辑都放到一个web页面中，根据路由的变化替换对应的内容和逻辑。在传统的web项目中，路由往往是由服务器端控制，所以SPA的实现基础就是路由逻辑前端化，由前端代码在浏览器中控制。

## 路由模式

1、hash 模式的实现原理
**原理：通过监听hashchange事件来监测hash值变化，然后在回调函数中匹配hash做相应的页面更新操作，从而实现前端路由。**
vue-router 默认 hash 模式——使用URL的hash来模拟一个完整的URL，于是当URL改变时，页面不会重新加载。hash（#）是URL 的锚点，代表的是网页中的一个位置，单改变#后的部分，浏览器只会滚动到相应位置，不会重新加载网页，也就是说hash 出现在 URL 中，但不会被包含在 http 请求中，对后端完全没有影响，因此改变 hash 不会重新加载页面；同时每一次改变#后的部分，都会在浏览器的访问历史中增加一个记录，使用”后退”按钮，就可以回到上一个位置；所以说Hash模式通过锚点值的改变，根据不同的值，渲染指定DOM位置的不同数据。hash模式的原理是onhashchange事件(监测hash值变化)，可以在window对象上监听这个事件。我们可以使用 hashchange 事件来监听 hash 值的变化，从而对页面进行跳转（渲染）。

2. history 模式的实现原理

**原理：利用HTML5的history对象新增的pushState()与replaceState()方法实现改变url地址且不会发送请求。通过设置监听器获取url的变化，然后再进行相应的页面更新操作，来实现前端路由。**这个实现需要服务器的支持，需要把所有路由都重定向到根页面。
由于hash模式会在url中自带#，如果希望url更优雅时，可以使用history模式，只需要在配置路由规则时，加入”mode: “history”, 这种模式充分利用了html5, historyinterface中新增的pushState() 和 replaceState() 方法。这两个方法是用于浏览器记录栈，在当前已有的 back、forward、go 基础之上，它们提供了对历史记录修改的功能。只是当它们执行修改时，虽然改变了当前的 URL ，但浏览器不会立即向后端发送请求。所以你要在服务端增加一个覆盖所有情况的候选资源：如果URL匹配不到任何静态资源，则应该返回同一个index.html页面，这个页面就是你app依赖的页面。（这种模式需要在服务端进行匹配设置，如果url匹配不到相应的资源，就返回同一index.html页面）
mode: 'history'
window.history.pushState(null, null, path);
window.history.replaceState(null, null, path);

# vuex

Vuex 是一个专为 Vue.js 应用程序开发的状态管理模式。每一个 Vuex 应用的核心就是 store（仓库）。“store” 基本上就是一个容器，它包含着你的应用中大部分的状态 ( state )。

Vuex 的状态存储是响应式的。当 Vue 组件从 store 中读取状态的时候，若 store 中的状态发生变化，那么相应的组件也会相应地得到高效更新。

改变 store 中的状态的唯一途径就是显式地提交 (commit) mutation。这样使得我们可以方便地跟踪每一个状态的变化。

场景：多个组件共享数据或者是跨组件传递数据时

vuex的流程

页面通过mapAction异步提交事件到action。action通过commit把对应参数同步提交到mutation，mutation会修改state中对应的值。最后通过getter把对应值跑出去，在页面的计算属性中，通过，mapGetter来动态获取state中的值

state：vuex的基本数据，用来存储变量；

mutation：提交更新数据的方法，在里面更改state中的数据

1.区别：**vuex存储在内存**，localstorage（本地存储）则以文件的方式存储在本地,永久保存；sessionstorage( 会话存储 ) ,临时保存。localStorage和sessionStorage只能存储字符串类型，对于复杂的对象可以使用ECMAScript提供的JSON对象的stringify和parse来处理

# 响应式原理

Vue是采用数据劫持结合发布/订阅模式的方式，通过Object.defineProperty()来劫持各个属性的setter，getter，在数据变动时发布消息给订阅者，触发相应的监听回调。

在生成vue实例时，为对传入的data进行遍历，使用`Object.defineProperty`把这些属性转为`getter/setter`，data 中声明的属性都被添加了访问器属性，当读取 data 中的数据时自动调用 get 方法，当修改 data 中的数据时，自动调用 set 方法，.每个vue实例都有一个watcher实例，它会在实例渲染时记录这些属性，并在setter触发时重新渲染。

# mvvm

#### MVVM 基本定义

1.MVVM 即 Model-View-ViewModel 的简写。即模型-视图-视图模型。

2.模型（Model） 指的是后端传递的数据。

3.视图(View)指的是所看到的页面。

4.视图模型(ViewModel)是 mvvm 模式的核心，它是连接 view 和 model 的桥梁。它有两个方向：

一是将模型（Model）转化成视图 (View)，即将后端传递的数据转化成所看到的页面。实现的方式是：数据绑定。

 二是将视图 (View)转化成模型(Model)，即将所看到的页面转化成后端的数据。实现的方式是：DOM 事件 监听。这两个方向都实现的，我们称之为数据的双向绑定。

#### MVC 基本定义

1.MVC 基本定义 MVC 是 Model-View- Controller 的简写。即模型-视图-控制器。M 和 V 指的意思和 MVVM 中的 M 和 V 意思一样。C 即 Controller 指的是页面业务逻辑。

2.使用 MVC 的目的就是将 M 和 V 的代码分离。MVC 是单向通信。也就是 View 跟 Model，必须通过 Controller 来承上启 下。

3.MVVM 实 现的是业务逻辑组件的重用，使开发更高效，结构更清晰，增加代码的复用性。

# conputed和watch

computed： 是计算属性，依赖其它属性值，并且 computed 的值有缓存，只有它依赖的属性值发生改变，下一次获取 computed 的值时才会重新计算 computed 的值；

watch：主要是「观察」的作用，类似于某些数据的监听回调，每当监听的数据变化时都会执行回调进行后续操作；

**watcher** 是 data中每个数据的监听回调，当依赖的 data 的数据变化，执行回调，在方法中会传入 newVal 和 oldVal。

Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性。

从使用场景上说，computed 适用一个数据被多个数据影响，而 watch 适用一个数据影响多个数据。

**区别**：methods->computed->watch逐步响应式。methods每次调用每次执行；computed有缓存机制，只要对应data中数据没变，多次调用只执行一次；watch只要数据改变就会自动执行回调。

# 父子组件的生命周期

在父子组件中分别打印日志，可以得出以下执行顺序。

1.1.挂载阶段
该过程主要涉及 beforeCreate、created、beforeMount、mounted 4 个钩子函数。执行顺序为：
父beforeCreate -> 父created -> 父beforeMount -> 子beforeCreate -> 子created -> 子beforeMount -> 子mounted -> 父mounted
一定得等子组件挂载完毕后，父组件才能挂在完毕，所以父组件的 mounted 在最后。

1.2.更新阶段
该过程主要涉及 beforeUpdate、updated 2 个钩子函数。注意，当父子组件有数据传递时，才有这个更新阶段执行顺序的比较。执行顺序为：
父beforeUpdate -> 子beforeUpdate -> 子updated -> 父updated

1.3.销毁阶段
该过程主要涉及beforeDestroy、destroyed 2 个钩子函数。执行顺序为：
父beforeDestroy -> 子beforeDestroy -> 子destroyed -> 父destroyed

1.4.总结
Vue 父子组件生命周期钩子的执行顺序遵循：从外到内，再从内到外。

# 虚拟DOM和diff算法

## diff算法

\1.    diff算法是虚拟DOM技术的必然产物:通过新旧虚拟DOM作对比(即diff)，将变化的地方更新在真实DOM上;另外，也需要diff高效的执行对比过程，从而降低时间复杂度为O(n).

\2.    vue 2.x中为了降低Watcher粒度，每个组件只有一个Watcher与之对应，只有引入diff才能精确找到发生变化的地方。

\3.    vue中diff执行的时刻是组件实例执行其更新函数时，它会比对上一次渲染结果oldVnode和新的渲染结果newVnode，此过程称为patch。给真实的DOM打补丁

\4.    当数据发生改变时，set方法会让调用Dep.notify通知所有订阅者Watcher，订阅者就会调用patch给真实的DOM打补丁，更新相应的视图。

\5.    diff过程整体遵循深度优先、同层比较的策略;两个节点之间比较会根据它们是否拥有子节点或者文本节点做不同操作。首先假设头尾节点可能相同做4次比对尝试，如果没有找到相同节点才按照通用方式遍历查找，查找结束再按情况处理剩下的节点; 借助key通常可以非常精确找到相同节点，因此整个patch过程非常高效。

头尾比较4种情况

 let oldStartVnode = oldCh[0]

 let oldEndVnode = oldCh[oldEndIdx]

 let newStartVnode = newCh[0]

 let newEndVnode = newCh[newEndIdx]

两个开头相同，则执行patchVnode，

旧的结束和新的结束相同

老的开始和新的结束相同，除了打补丁之外还要移动到队尾

老的结束和新的开始相同

# 1． key的作用

主要是为了高效的更新虚拟DOM，其原理是在Vue源码里，vue在patch过程中会执行patchVnode，patchVnode里会执行updateChildren方法，它会更新所有的两个新旧子元素，在这个过程中就可以通过key可以精准判断两个节点是否是同一个，因为一般元素不会发生太大的变化，在判断过程就会很快的结束循环，从而避免频繁更新不同元素，使得整个patch过程更加高效，减少DOM操量，提高性能。如果不加key，在源码里会永远认为是相同的节点，这样就只能强制频繁的更新，就无法避免频繁更新，就导致做了很多额外的DOM操作，降低性能。



**methods**：每次调用每次执行；是函数调用，没有缓存功能。只要对应data中数据没变，多次调用只执行一次；watch只要数据改变就会自动执行回调。

**computed**：是属性调用，计算属性，具有缓存功能，依赖于data中的数据，只有在它的相关依赖数据发生改变时才会重新求值。computed其实是既可以当做属性访问也可以当做方法访问。computed可以防止文本插值中逻辑过重，导致不易维护

**watcher** 是 data中每个数据的监听回调，当依赖的 data 的数据变化，执行回调，在方法中会传入 newVal 和 oldVal。

Vue 实例将会在实例化时调用 $watch()，遍历 watch 对象的每一个属性。

从使用场景上说，computed 适用一个数据被多个数据影响，而 watch 适用一个数据影响多个数据。

**区别**：methods->computed->watch逐步响应式。methods每次调用每次执行；computed有缓存机制，只要对应data中数据没变，多次调用只执行一次；watch只要数据改变就会自动执行回调。c
