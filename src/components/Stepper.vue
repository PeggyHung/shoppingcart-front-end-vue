<template>
  <section class="checkout-stepper">
    <h2>結帳</h2>
    <div id="step-control" class="stepper-panel">
      <div class="container stepper-container">
        <div class="step left" :class="isStep1">
          <div class="circle-container"></div>
          <div class="label-container">寄送地址</div>
          <span class="connect-line"></span>
        </div>
        <div class="step" :class="isStep2">
          <div class="circle-container"></div>
          <div class="label-container">運送方式</div>
          <span class="connect-line"></span>
        </div>
        <div class="step right" :class="isStep3">
          <div class="circle-container"></div>
          <div class="label-container">付款資訊</div>
        </div>
      </div>
    </div>
  </section>
</template>

<script>
export default {
  data() {
    return{
    isStep1: "active",
    isStep2: "",
    isStep3: "",
    };
  },
  methods: {
    next(index) {
      if (index === 1){
        this.isStep1 = "active";
        this.isStep2 = "";
        this.isStep3 = "";
        console.log(index)
      } else if(index === 2){
        this.isStep1 = "checked";
        this.isStep2 = "active";
        this.isStep3 = "";
        console.log(index)
      } else{
        this.isStep1 = "checked";
        this.isStep2 = "checked";
        this.isStep3 = "active";
        console.log(index)
      }      
    }
  }
}
</script>