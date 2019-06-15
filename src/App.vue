<template>
  <div id="app">
    <MsAlert ref="msAlert" />
    <button class="btn btn-info" @click="openAlert">打開彈窗</button>
    <div class="status">{{alertStatus}}</div>
  </div>
</template>

<script>
import MsAlert from "@/components/Alert";

export default {
  name: "app",
  data() {
    return {
      alertStatus: ""
    };
  },
  components: {
    MsAlert
  },
  methods: {
    // 打開彈窗並傳入自訂配置
    openAlert() {
      var setting = {
        title: "你確定刪除嗎?",
        content: "刪除後將無法恢復...",
        onConfirm: this.alertConfirm,
        onCancel: this.alertCancel
      };

      this.$refs.msAlert.alert(setting);
    },
    // 傳入取消後要觸發的方法
    alertCancel() {
      console.log("取消 關閉");
      this.alertStatus = "你點擊了取消";
    },
    // 傳入確認後要觸發的方法
    alertConfirm() {
      console.log("確認... 發送api");
      this.alertStatus = "你點擊了確認";
    }
  }
};
</script>

<style lang="scss">
$colorPrimary: #3498db;
$colorGray: #34495e;

#app {
  font-family: "Avenir", Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  color: #2c3e50;
  height: 100vh;
  width: 100vw;
  display: flex;
  flex-flow: column nowrap;
  justify-content: center;
  align-items: center;
  text-align: center;
}

.btn {
  padding: 10px 25px;
  font-size: 16px;
  border-radius: 2px;
  border: none;
  cursor: pointer;
  outline: none;
  background-color: $colorPrimary;
  color: #fff;
  letter-spacing: 1px;
  box-shadow: 0 10px 20px 0 rgba(black, 0.125);
}

.status {
  border: solid 2px $colorGray;
  margin-top: 50px;
  min-width: 150px;
  height: 60px;
  line-height: 60px;
  color: $colorGray;
  font-size: 16px;
  font-weight: bold;
  letter-spacing: 1px;
}
</style>
