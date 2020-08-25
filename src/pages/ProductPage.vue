<template>
  <div class="product-page">
    <h1>PRODUCT PAGE</h1>
    <div v-if="this.visibleProduct" class="product-container">
      <div class="img-container big">
        <div class="img big"></div>
      </div>
      <div class="product-info">
        <p>{{ this.visibleProduct.brand }}</p>
        <h2 class="product-name">
          {{ this.visibleProduct.name }}
          <span class="small-title">
            - model:
            {{ this.visibleProduct.model }}
          </span>
          {{ this.visibleProduct.special ? "*" : null }}
        </h2>
        <p>
          ${{
            (
              this.visibleProduct.price * 0.23 +
              this.visibleProduct.price
            ).toFixed(2)
          }}
          (incl. VAT)
        </p>
        <p>
          Color: <strong>{{ this.visibleProduct.color }}</strong>
        </p>
        <ul class="product-additional-list">
          <li>
            <button @click="this.setDescReveal">
              <span>Description</span><span class="rotate">^</span>
            </button>
            <div
              class="desc-container"
              :class="this.descReveal ? 'open' : null"
            >
              <p v-if="this.descReveal">
                {{ this.visibleProduct.description }}
              </p>
            </div>
          </li>
        </ul>
      </div>
    </div>
  </div>
</template>

<script>
import { mapState } from "vuex";

export default {
  name: "ProductPage",
  props: {
    id: Number,
  },
  data: function() {
    return {
      visibleProduct: null,
      descReveal: false,
    };
  },
  computed: {
    ...mapState(["products"]),
  },
  methods: {
    setDescReveal() {
      this.descReveal = !this.descReveal;
    },
  },
  created: function() {
    this.products.map((product) => {
      if (product.id === this.id) {
        this.visibleProduct = product;
      }
    });
  },
};
</script>

<style scoped>
.product-container {
  display: flex;
  justify-content: space-between;
}

.product-container > * {
  flex: 1;
}

.product-additional-list {
  margin: 0;
  padding: 0;
  list-style: none;
}

.product-additional-list li {
  border-top: 1px solid rgba(0, 0, 0, 0.34);
  border-bottom: 1px solid rgba(0, 0, 0, 0.34);
  text-align: center;
  display: flex;
  flex-flow: column;
  align-items: center;
  justify-content: center;
}

.product-additional-list li button {
  display: flex;
  justify-content: space-between;
  align-items: center;
  background: none;
  border: none;
  width: 100%;
  height: 50px;
  font-weight: bold;
  cursor: pointer;
}

.product-additional-list li button:focus {
  outline: none;
}

.product-additional-list li .desc-container {
  overflow: hidden;
  max-height: 0;
  transition: all 0.5s;
}

.product-additional-list li .desc-container.open {
  max-height: 500px;
}

.product-additional-list button .rotate {
  transform: rotate(180deg);
}

.img-container {
  margin-right: 1rem;
}

.img {
  height: 400px;
  width: 400px;
}

.img::before,
.img::after {
  height: 566px;
}

.product-info {
  margin: 0 auto;
  margin-left: 1rem;
  text-align: left;
}

.product-name {
  text-transform: uppercase;
}

.small-title {
  text-transform: lowercase;
  font-size: 1.4rem;
}
</style>