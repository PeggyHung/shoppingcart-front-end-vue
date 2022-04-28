<template>
  <section class="shopping-cart">
    <h2>購物籃</h2>
    <div class="cart-list">
      <div class="product" v-for="product in products" :key="product.id">
        <img :src="product.image" alt="" />
        <div class="product-info">
          <h5 class="product-name">{{ product.name }}</h5>
          <div class="product-number">
            <p hidden>{{ product.singlePrice }}</p>
            <span @click="clickminus(product.id)">
              <i class="fas fa-minus-circle"></i>
            </span>
            <p>{{ product.amount }}</p>
            <span @click="clickplus(product.id)">
              <i class="fas fa-plus-circle"></i>
            </span>
          </div>
          <h5 class="product-price">{{ product.price }}</h5>
        </div>
      </div>
      <hr />
      <div class="shipping-fee">
        <p class="shipping-fee-title">運費</p>
        <p class="shipping-fee-price">{{shipFee}}</p>
      </div>
      <hr />
      <div class="total-cost">
        <p class="total-cost-title">小計</p>
        <p class="total-cost-price">{{ calculateCost() }}</p>
      </div>
    </div>
  </section>
</template>

<script>
const productsInfo = [
  {
    id: 1,
    name: "破壞補丁修身牛仔褲",
    price: "$3,999",
    singlePrice: 3999,
    amount: 1,
    image: "https://img.onl/9HOcgr",
  },
  {
    id: 2,
    name: "刷色直筒牛仔褲",
    price: "$1,299",
    singlePrice: 1299,
    amount: 1,
    image: "https://img.onl/Kcu4Uz",
  },
];

export default {
  props: {
    shipFee : String,
  },
  data() {
    return {
      products: [],      
    };
  },
  created() {
    this.fetchProducts();
  },
  methods: {
    fetchProducts() {
      this.products = productsInfo;
    },    
    clickplus(id) {
      console.log(id);
      this.products[id - 1].amount++;
      let mutiplePrice =
        this.products[id - 1].singlePrice * this.products[id - 1].amount;
      this.products[id - 1].price = "$" + mutiplePrice.toLocaleString("en-US");
    },
    clickminus(id) {
      console.log(id);
      if (this.products[id - 1].amount > 0) {
        this.products[id - 1].amount--;
      }
      let mutiplePrice =
        this.products[id - 1].singlePrice * this.products[id - 1].amount;
      this.products[id - 1].price = "$" + mutiplePrice.toLocaleString("en-US");
    },
    calculateCost() {
      let totalCost = 0;
      for (let i = 0; i < this.products.length; i++) {
        totalCost += this.products[i].singlePrice * this.products[i].amount;
      }
      if (this.shipFee !== "免費") totalCost += 500;

      return "$" + totalCost.toLocaleString("en-US");
    },
  },
};
</script>