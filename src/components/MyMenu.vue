<!--
 * @Description: 菜单组件，用于首页商品展示模块的右上角菜单
 * @Author: hai-27
 * @Date: 2020-02-07 16:23:00
 * @LastEditors: hai-27
 * @LastEditTime: 2020-02-26 22:52:35
 -->
<template>
  <div class="myMenu" id="myMenu">
    <ul>
      <li
        v-for="item in val"
        :key="item"
        :class="activeClass == item ? 'active':''"
        @mouseover="mouseover($event,item)"
      >
        <router-link to>
          <slot :name="item"></slot>
        </router-link>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  props: ["val"],
  name: "MyMenu",
  data() {
    return {
      activeClass: 1
    };
  },
  methods: {
    // 通过mouseover事件控制当前显示的商品分类，1为该类别的热门商品
    mouseover(e, val) {
      this.activeClass = val;
    }
  },
  watch: {
    // 向父组件传过去当前要显示的商品分类，从而更新商品列表
    activeClass: function(val) {
      this.$emit("fromChild", val);
    }
  }
};
</script>
<style scoped>
#myMenu li {
  float: left;
  margin-left: 30px;
}

#myMenu a:hover {
  color: #ff6700;
  border-bottom: 2px solid #ff6700;
}

#myMenu .active a {
  color: #ff6700;
  border-bottom: 2px solid #ff6700;
}
</style>