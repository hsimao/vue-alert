<template>
  <transition name="ms-transition" mode="out-in"
    appear>
    <div class="ms-alert" v-show="isAction">
      <div class="ms-alert__content">
        <h2 class="ms-alert__content__title">{{title}}</h2>
        <p class="ms-alert__content__text">{{content}}</p>
        <div class="alert__content__btns">
          <button class="ms-alert__btn" @click="handleClick(false)">{{cancelBtnText}}</button>
          <button class="ms-alert__btn" @click="handleClick(true)">{{confirmBtnText}}</button>
        </div>
      </div>
    </div>
  </transition>
</template>

<script>
export default {
  name: "ms-alert",
  data() {
    return {
      isAction: false,
      onConfirm: false,
      onCancel: false,
      cancelBtnText: "取消",
      confirmBtnText: "確認",
      title: "標題",
      content: "內容.."
    };
  },
  methods: {
    handleClick(type) {
      this.isAction = false;
      if (type) {
        if (this.onConfirm) this.onConfirm();
      } else {
        if (this.onCancel) this.onCancel();
      }
      this.onConfirm = false;
      this.onCancel = false;
    },
    alert(setting) {
      this.title = setting.title || "標題";
      this.content = setting.content || "內容";
      this.onConfirm = setting.onConfirm || false;
      this.onCancel = setting.onCancel || false;
      this.isAction = true;
      // 鎖屏, 限制 body scroll
      document.body.style.overflow = "hidden";
    }
  }
};
</script>

<style lang="scss" src="./style.scss" scoped></style>