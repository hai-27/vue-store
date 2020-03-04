<!--
 * @Description: 列表组件，用于首页、全部商品页面的商品列表
 * @Author: hai-27
 * @Date: 2020-02-07 16:23:00
 * @LastEditors: hai-27
 * @LastEditTime: 2020-03-04 23:37:54
 -->
<template>
  <div id="myList" class="myList">
    <ul>
      <li v-for="item in list" :key="item.product_id">
        <i class="el-icon-close delete" v-show="isDelete" @click="deleteCollect(item.product_id)"></i>
        <router-link :to="{ path: '/goods/details', query: {productID:item.product_id} }">
          <img :src="$target +item.product_picture" alt />
          <h2>{{item.product_name}}</h2>
          <h3>{{item.product_title}}</h3>
          <p>
            <span>{{item.product_selling_price}}元</span>
            <span
              v-show="item.product_price != item.product_selling_price"
              class="del"
            >{{item.product_price}}元</span>
          </p>
        </router-link>
      </li>
      <li v-show="isMore && list.length>=1" id="more">
        <router-link :to="{ path: '/goods', query: {categoryID:categoryID} }">
          浏览更多
          <i class="el-icon-d-arrow-right"></i>
        </router-link>
      </li>
    </ul>
  </div>
</template>
<script>
export default {
  name: "MyList",
  // list为父组件传过来的商品列表
  // isMore为是否显示“浏览更多”
  props: ["list", "isMore", "isDelete"],
  data() {
    return {};
  },
  computed: {
    // 通过list获取当前显示的商品的分类ID，用于“浏览更多”链接的参数
    categoryID: function() {
      let categoryID = [];
      if (this.list != "") {
        for (let i = 0; i < this.list.length; i++) {
          const id = this.list[i].category_id;
          if (!categoryID.includes(id)) {
            categoryID.push(id);
          }
        }
      }
      return categoryID;
    }
  },
  methods: {
    deleteCollect(product_id) {
      this.$axios
        .post("/api/user/collect/deleteCollect", {
          user_id: this.$store.getters.getUser.user_id,
          product_id: product_id
        })
        .then(res => {
          switch (res.data.code) {
            case "001":
              // 删除成功
              // 提示删除成功信息
              this.notifySucceed(res.data.msg);
              this.$router.push({ path: "/collect" });
              break;
            default:
              // 提示删除失败信息
              this.notifyError(res.data.msg);
          }
        })
        .catch(err => {
          return Promise.reject(err);
        });
    }
  }
};
</script>
<style scoped>
.myList ul li {
  z-index: 1;
  float: left;
  width: 234px;
  height: 280px;
  padding: 10px 0;
  margin: 0 0 14.5px 13.7px;
  background-color: white;
  -webkit-transition: all 0.2s linear;
  transition: all 0.2s linear;
}
.myList ul li:hover {
  z-index: 2;
  -webkit-box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
  box-shadow: 0 15px 30px rgba(0, 0, 0, 0.1);
  -webkit-transform: translate3d(0, -2px, 0);
  transform: translate3d(0, -2px, 0);
}
.myList ul li img {
  width: 160px;
  display: block;
  margin: 0 auto;
}
.myList ul li h2 {
  margin: 25px 10px 0;
  font-size: 14px;
  font-weight: 400;
  color: #333;
  text-align: center;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
.myList ul li h3 {
  margin: 5px 10px;
  height: 18px;
  font-size: 12px;
  font-weight: 400;
  color: #b0b0b0;
  text-align: center;
  text-overflow: ellipsis;
  white-space: nowrap;
  overflow: hidden;
}
.myList ul li p {
  margin: 10px 10px 10px;
  text-align: center;
  color: #ff6700;
}
.myList ul li p .del {
  margin-left: 0.5em;
  color: #b0b0b0;
  text-decoration: line-through;
}
.myList #more {
  text-align: center;
  line-height: 280px;
}
.myList #more a {
  font-size: 18px;
  color: #333;
}
.myList #more a:hover {
  color: #ff6700;
}
.myList ul li .delete {
  position: absolute;
  top: 10px;
  right: 10px;
}
.myList ul li .delete:hover {
  color: #ff6700;
}
</style>