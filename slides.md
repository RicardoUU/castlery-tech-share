---
background: /bg.png
class: text-center
highlighter: shiki
lineNumbers: false
info: |
  ## Slidev Starter Template
  # Presentation slides for developers.

  Learn more at [Sli.dev](https://sli.dev)
drawings:
  persist: falser
css: unocss
title: 前端领域驱动设计(DDD)
---

# 前端领域驱动设计(DDD)

<!-- Presentation slides for developers -->

<div class="abs-br m-6 flex gap-2">
  <button @click="$slidev.nav.openInEditor()" title="Open in Editor" class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon:edit />
  </button>
  <a href="https://github.com/slidevjs/slidev" target="_blank" alt="GitHub"
    class="text-xl icon-btn opacity-50 !border-none !hover:text-white">
    <carbon-logo-github />
  </a>
</div>

<!--
The last comment block of each slide will be treated as slide notes. It will be visible and editable in Presenter Mode along with the slide. [Read more in the docs](https://sli.dev/guide/syntax.html#notes)
-->

<style>
h1 {
  margin-bottom: 200px !important;
  color: #fff !important;
  background-color: #fff !important;
  background-image: none;

}
</style>

---

# 什么是领域驱动设计?

<h2 class="text-center mt-20 mb-10"> 为什么需要DDD </h2>

<v-click>

- 业务复杂度失控
- 技术架构/模型和业务模型 不匹配
- 知识的丢失：**上一任** 人走了,代码留下了，知识没留下。 外包出去的应用，代码回来了，知识没回来。

</v-click>

<!-- 
随着业务的迭代，你会发现代码迭代着迭代着就**改不动了**，最后啊 不得不另起炉灶。归根结底无非就是业务的复杂性在代码应用中失控了。
我们设计的 技术模型 与 领域模型 不匹配。于是每次需求的改动，映射到技术模型的改动可能就是极大的工作量。甚至根本改不动，在业务压力很大的时候，我们只能告诉产品经理，这个可以做，但是我们需要2个月。结局很可能就是需求方的妥协，牺牲用户的利益。导致产品越来越难用。
 -->
---

# 什么是领域驱动设计?

<!-- Slidev is a slides maker and presenter designed for developers, consist of the following features -->
<h2 class="text-center mt-40"> 先谈谈MVC & MVVM </h2>
<!--
You can have `style` tag in markdown to override the style for the current page.
Learn more: https://sli.dev/guide/syntax#embedded-styles
-->

<style>
h2 {
}
</style>

<!--
在了解前端的领域驱动设计之前可以先从 MVC && MVVM 模式开始，无论是MVC还是MVVM 都是为了从模式设计层面去和业务更好的匹配，然而在这两者的还有一个共同的不足之处就是在于如何去划分 M V C && M V V M。通常在划分的与实际业务有偏差时就会出现一个情况：随着业务的迭代，慢慢的就会发现来了新的需求需要做过去重复做过的事情 亦或是 一个改动就会触发全局的改动，很难去做迭代。
-->

---

# 什么是领域驱动设计？

<h2 class="text-center mt-40"> 组件驱动设计(CDD) </h2>

<!-- [Fortress](https://fan-powder-159.notion.site/Design-System-Fortress-6a9343509f664a1e8825a1e24c2358bf) -->

<div
  v-motion
  :initial="{ x:35, y: 40, opacity: 0}"
  :enter="{ y: 200, opacity: 1, transition: { delay: 3500 } }">

[Fortress](https://fan-powder-159.notion.site/Design-System-Fortress-6a9343509f664a1e8825a1e24c2358bf)

</div>
<!--
它是一种开发方法，它围绕组件构建项目。是一个自下而上构建UI的过程，从原子级别的组件开始，到整体的页面级别结束。
然后CDD仍然有一个缺点：它是面向原子化的，这是描述了页面的构成组件，如果在代码设计的不合理的情况下依然会出现代码、架构、等等等设计与实际业务不符的情况。但是在目前的前端体系中，CDD已经能解决大部分的业务问题了。
-->

---

# 什么是领域驱动设计？


<h2 class="text-center mt-40"> 微服务 & 微前端 </h2>

<!--
微服务和微前端的一个共同思想：分治。
从业务角度上来看，就是把一个大的业务分成小的业务模块，已解决整个业务系统的问题，在所谓的大厂里的标配通常是：微服务+业务中台。
而微前端算是借鉴了微服务的思想，在前端中 把一个大的前端应用系统通过业务划分，分成多个小的前端应用 然后在主应用当中去通过一些方式去加载渲染这些微前端应用。 这些微应用可以在不同的团队、项目当中去维护。
然而这两者依然有一个问题：如何去划分微服务和微应用？这就是DDD解决的问题。
-->

---

# 领域驱动设计

<div grid="~ cols-2 gap-4">
<div>

> 在维基百科中定义：领域驱动设计是一种由 域模型 来驱动着系统设计的思想，不是通过存储数据词典(DB表字段、ESMapper字段等等)来驱动系统设计。 领域模型是对业务模型的抽象， DDD 是把业务模型翻译成系统架构设计的一种方式。
<div class="my-10"></div>

- 领域即“边界”
- 领域即业务的抽象化表达方式
- 领域驱动设计的核心思想是**分治** 、 **聚合**
</div>

<div>
领域的特点

> 来自 掘金：头号前端 
- **领域层是 稳定 的**（页面以及与页面绑定的模块都是不稳定的）。
- **领域层是 解耦 的**（页面是会耦合的，页面的数据会来自多个接口，多个领域）。
- **领域层具有 极高复杂度** ，值得单独管理(view层处理页面渲染以及页面逻辑控制，复杂度已经够高，领域层解耦可以轻view层。 view层尽可能轻量。
- **领域层 以层为单位 是可以被 复用 的**（你的代码可能会抛弃某个技术体系，从vue转成react，或者可能会推出一个移动版，在这些情况下，领域层这一层都是可以直接复用）

</div>
</div>

<!--
你可以很明显的感知到，“领域”意味着“边界”，意味着某些“共性”和某些“特性”。
<p>
DDD的思想与微服务和微前端的思想类似，这就是为什么在一些团队中通常把他们结合应用。
</p>
-->

---
class: px-20
---

# 如何在前端中实践应用DDD

前端相比于后端更复杂

<img
  src="/fetable.png"
/>


---
preload: false
---

# 如何在前端中实践应用DDD

<img
  src="/liucheng.jpg"
  height="300px"
/>

<style>
  img {
    width: 500px;
  }
</style>

<!--
其中有两个关键点是统一语言、领域模型
-->

---

# 如何在前端中实践应用DDD


<h2 class="text-center mt-40"> 关于 统一语言 </h2>


<!-- ddd首要的核心是一个项目要形成客户、产品、开发、测试各方一致的通用语言，用来描述业务。也就是说要有一套业务术语体系，这套术语名词要应用于产品需求沟通，功能描述，测试编写，函数和变量命名等所有相关环节。这个事情是项目整体层面的，前端只是其中一小部分，也就是说前端要使用ddd所形成的通用术语体系。
-->

---

# 如何在前端中实践应用DDD

<h2 class="text-center mt-20"> 如何建立领域模型 </h2>

- 充分理解业务
- **横纵**划分法

<!--
<p> 领域驱动模型描述的是业务，所以实现DDD就需要充分理解业务。 </p>
<p>横纵划分就好比一块肉，横切竖切就能得到一小块肉。而这里的横纵指的是 横向领域和纵向领域。</p>
-->

---

# 如何在前端中实践应用DDD

<h2 class="text-center mt-40"> OK，前面都是废话，来看项目结构 </h2>


---

# 如何在前端中实践应用DDD

- 一个文件夹包含该领域内所有逻辑（视图，样式，测试，状态，接口），禁止将逻辑放置于文件夹以外
- 每个domain只包含一下几种文件/文件夹, 结合 hooks来做到相关状态逻辑收敛与复用： 
  - **components (领域内的组件)**
  - **containers (子领域)**
  - **helpers (工具函数)**
  - **hooks**
  - **store** redux等状态管理
  - **services** 
  - **types** 
  - **constants.ts** (静态变量)
  - **_tests_** (测试相关)
  - **index.ts (入口)**
- 如果需要由其他领域调用(利用控制反转（依赖注入）SOA 进行组合), 可以通过接口暴露，在其他领域中引用。

---
layout: center
class: text-center
---

# 最后

<h2>DDD强调的是设计而不是架构，设计是不分前后端的</h2>
<br>
<!-- <h2>感谢Slidev</h2> -->


