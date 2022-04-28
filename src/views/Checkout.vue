<template>
  <main class="main-container">
    <Stepper ref="stepperRef" />
    <Form ref="formRef" @afterpayclick="payclick" />
    <Btn
      ref="btnRef"
      @after-click="handleAfterClick"
      @before-click="handleBeforeClick"
    />
    <Cart ref="cartRef" :shipFee="shipPrice" />
  </main>
</template>

<script>
import Stepper from "./../components/Stepper";
import Form from "./../components/Form";
import Btn from "./../components/Btn";
import Cart from "./../components/Cart";

let number = 1;

export default {
  components: {
    Stepper,
    Form,
    Btn,
    Cart,
  },
  data() {
    return {
     shipPrice: "免費",
    };
  },
  methods: {
    handleAfterClick() {
      console.log("next");
      if (number < 3) number++;
      this.$refs.stepperRef.next(number);
      this.$refs.formRef.changeForm(number);
      this.$refs.btnRef.changePage(number);
    },
    handleBeforeClick() {
      console.log("before");
      if (number > 1) number--;
      this.$refs.stepperRef.next(number);
      this.$refs.formRef.changeForm(number);
      this.$refs.btnRef.changePage(number);
    },
    payclick(money) {
      this.shipPrice = money === 0 ? "免費" : "500";
    },
  },
};
</script>

<style lang="scss" src="./../scss/style.scss"></style>