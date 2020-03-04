<!--
 * @Description: 我的收藏页面组件
 * @Author: hai-27
 * @Date: 2020-02-20 17:22:56
 * @LastEditors: hai-27
 * @LastEditTime: 2020-03-04 23:33:48
 -->
<template>
  <div class="collect">
    <!-- Add a static page for my favorite module -->
    <div class="collect-header">
      <div class="collect-title">
        <i class="el-icon-collection-tag" style="color: #ff6700;"></i>
        我的收藏
      </div>
    </div>
    <div class="content">
      <div class="goods-list">
        <MyList :list="collectList" :isDelete="true"></MyList>
      </div>
    </div>
  </div>
</template>
<script>
export default {
  data() {
    return {
      collectList: []
    };
  },
  activated() {
    // 获取收藏数据
    this.$axios
      .post("/api/user/collect/getCollect", {
        user_id: this.$store.getters.getUser.user_id
      })
      .then(res => {
        if (res.data.code === "001") {
          this.collectList = res.data.collectList;
        } else {
          this.notifyError(res.data.msg);
        }
      })
      .catch(err => {
        return Promise.reject(err);
      });
  }
};
</script>
<style scoped>
.collect {
  background-color: #f5f5f5;
}
.collect .collect-header {
  height: 64px;
  background-color: #fff;
  border-bottom: 2px solid #ff6700;
}
.collect .collect-header .collect-title {
  width: 1225px;
  margin: 0 auto;
  height: 64px;
  line-height: 64px;
  font-size: 28px;
}
.collect .content {
  padding: 20px 0;
  width: 1225px;
  margin: 0 auto;
}
.collect .content .goods-list {
  margin-left: -13.7px;
  overflow: hidden;
}
</style>