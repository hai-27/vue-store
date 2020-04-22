# Store（参考小米商城）

## 前言

2020年寒假尤其特殊，因为新型冠状病毒肺炎疫情，学校至今没有开学。想起上学期利用课余时间学习了`Vue.js`、`Node.js`，一直想做个完整的项目实战一下，但之前在学校并没有那么多的时间。现在恰好有时间，就想着做一个项目巩固之前学到的东西。

思来想去，最后决定模仿 [小米商城 ](www.mi.com)做一个电商项目。可能时间隔得有点久了，之前学的东西很多都差不多忘记了，做这个项目基本上都是看着官方的文档一点一点做的。在家里也免不了有各种各样的事情耽误了项目的进度。现在终于差不多做好了，分享出来，新手上路，如有错误，请多多指教。

## 说明

> 本项目前后端分离，前端参考 [小米商城](www.mi.com) 实现，但与小米官方没有关系，纯属个人瞎搞，若需要购买小米产品请到小米官方商城。

> 这是本项目的前端，后端请移步到[store-server](https://github.com/hai-27/store-server) 。

> 前端已经部署在阿里云，欢迎访问 [http://106.15.179.105/](http://106.15.179.105/) （没有兼容移动端，请使用电脑访问）。

> 后端也已经部署在阿里云，接口地址已经修改为线上地址，本地运行前端也可以正常访问后端。

> 本人在读本科大三，今年暑假即将开始实习，后面的时间可能没有那么的自由，但会不定期的更新完善该项目，如有问题请直接在 Issues 中提。

> 如果觉得这个项目还不错，您可以点右上角 `Star`支持一下， 谢谢！ ^_^

## 项目简介

本项目前后端分离，前端基于`Vue`+`Vue-router`+`Vuex`+`Element-ui`+`Axios`，参考小米商城实现。后端基于`Node.js(Koa框架)`+`Mysql`实现。

前端包含了11个页面：首页、登录、注册、全部商品、商品详情页、关于我们、我的收藏、购物车、订单结算页面、我的订单以及错误处理页面。

实现了商品的展示、商品分类查询、关键字搜索商品、商品详细信息展示、登录、注册、用户购物车、订单结算、用户订单、用户收藏列表以及错误处理功能。

后端采取了MVC模式，根据前端需要的数据分模块设计了相应的接口、控制层、数据持久层。后端传送地址[store-server](https://github.com/hai-27/store-server) 。

## 技术栈

- **前端：**`Vue`+`Vue-router`+`Vuex`+`Element-ui`+`Axios`

- **后端：**`Node.js`、`Koa框架`

- **数据库：**`Mysql`

## 功能模块

### 登录

页面使用了element-ui的`Dialog`实现弹出蒙版对话框的效果，`登录`按钮设置在App.vue根组件，通过`vuex`中的`showLogin`状态控制登录框是否显示。

这样设计是为了既可以通过点击页面中的按钮登录，也可以是用户访问需要登录验证的页面或后端返回需要验证登录的提示后自动弹出登录框，减少了页面的跳转，简化用户操作。

用户输入的数据往往是不可靠的，所以本项目前后端都对登录信息进行了校验，前端基于element-ui的表单校验方式，自定义了校验规则进行校验。

### 注册

页面同样使用了element-ui的`Dialog`实现弹出蒙版对话框的效果，`注册`按钮设置在App.vue根组件，通过父子组件传值控制注册框是否显示。

用户输入的数据往往是不可靠的，所以本项目前后端同样都对注册信息进行了校验，前端基于element-ui的表单校验方式，自定义了校验规则进行校验。

### 首页

首页主要是对商品的展示，有轮播图展示推荐的商品，分类别对热门商品进行展示。

### 全部商品

全部商品页面集成了全部商品展示、商品分类查询，以及根据关键字搜索商品结果展示。

### 商品详情页

商品详情页主要是对某个商品的详细信息进行展示，用户可以在这里把喜欢的商品加入购物车或收藏列表。

### 我的购物车

购物车采用vuex实现，页面效果参考了小米商城的购物车。

详细实现过程请看：[基于Vuex实现小米商城购物车](https://juejin.im/post/5e660ef9518825490276748a)

### 订单结算

用户在购物车选择了准备购买的商品后，点击“去结算”按钮，会来到该页面。
用户在这里选择收货地址，确认订单的相关信息，然后确认购买。

### 我的收藏

用户在商品的详情页，可以通过点击加入 喜欢 按钮，把喜欢的商品加入到收藏列表。

### 我的订单

对用户的所有订单进行展示。

## 运行项目

**注意：**

- 后端接口地址已经修改为线上的地址，本地运行会直接分为我部署在服务器的后端。
- 为了方便测试，数据库数据没有加密，注册时切记**不要使用自己的常用密码**。
- 如果需要自己运行后端，请移步到[store-server](https://github.com/hai-27/store-server) clone后端项目，并修改前端的接口地址为您的服务器地址。

```
1. Clone project

git clone https://github.com/hai-27/vue-store.git

2. Project setup

cd vue-store
npm install

3. Compiles and hot-reloads for development

npm run serve

4. Compiles and minifies for production

npm run build
```
## 页面截图

**首页**

![](https://raw.githubusercontent.com/hai-27/vue-store/master/public/screenshots/home.png)

**全部商品**

![](https://raw.githubusercontent.com/hai-27/vue-store/master/public/screenshots/goods.png)

**购物车**

![](https://raw.githubusercontent.com/hai-27/vue-store/master/public/screenshots/shoppingCart.png)

**我的收藏**

![](https://raw.githubusercontent.com/hai-27/vue-store/master/public/screenshots/collect.png)

**我的订单**

![](https://raw.githubusercontent.com/hai-27/vue-store/master/public/screenshots/order.png)

**登录**

![](https://raw.githubusercontent.com/hai-27/vue-store/master/public/screenshots/login.png)

**注册**

![](https://raw.githubusercontent.com/hai-27/vue-store/master/public/screenshots/register.png)



**作者** [hai-27](https://github.com/hai-27)

2020年3月8日