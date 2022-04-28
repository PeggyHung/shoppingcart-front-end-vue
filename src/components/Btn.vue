<template>
  <section class="btn-wrapper">
    <hr />
    <div class="btn-control" :class="isBtn">
      <button class="btn btn-outline" @click.stop.prevent="prePage">
        上一步
      </button>
      <button class="btn btn-primary" @click.stop.prevent="nextPage">
        {{ btnText }}
      </button>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return {
      isBtn: "hidden",
      btnText: "下一步",
    };
  },
  methods: {
    nextPage() {
      this.$emit("after-click");
    },
    prePage() {
      this.$emit("before-click");
    },
    changePage(page) {
      this.isBtn = page === 1 ? "hidden" : "";
      this.btnText = page === 3 ? "送出申請" : "下一步";
    },
  },
};
</script>