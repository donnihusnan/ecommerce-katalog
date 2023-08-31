<template>
  <div class="home-page" :class="currentProductClass">
    <div v-if="isLoading">
      <Skeleton />
    </div>
    <div v-else-if="productAvailable" class="product">
      <img class="image" :src="currentProduct.image" />
      <div class="description">
        <h1>{{ currentProduct.title }}</h1>
        <h2>{{ currentProduct.category }}</h2>
        <hr />
        <p>{{ currentProduct.description }}</p>
        <hr />
        <h3>Price: ${{ currentProduct.price }}</h3>
        <button>Buy Now</button>
        <button @click="nextProduct">Next Product</button>
      </div>
    </div>
    <div v-else class="unavailable">
      <h3>This Product is unavailable to show</h3>
      <button @click="nextProduct">Next Product</button>
    </div>
  </div>
</template>

<script>
import Skeleton from '@/components/SkeletonLoading.vue';

export default {
  components: {
    Skeleton,
  },
  computed: {
    currentProductClass() {
      if (!this.currentProduct) return ''; // No product
      if (this.currentProduct.category === "men's clothing") {
        return 'men-section';
      } else if (this.currentProduct.category === "women's clothing") {
        return 'women-section';
      } else {
        return 'unavailable-product';
      }
    },
  },
  data() {
    return {
      products: [],
      currentIndex: 0,
      currentProduct: null,
      isLoading: false,
      productAvailable: true,
    };
  },
  mounted() {
    this.fetchProducts();
  },
  methods: {
    async fetchProducts() {
      try {
        this.isLoading = true;
        const response = await fetch('https://fakestoreapi.com/products');
        const data = await response.json();

        // Filter and store products with specific categories
        this.products = data;
        // .filter((product) => {
        //   return (
        //     product.category === "men's clothing" ||
        //     product.category === "women's clothing"
        //   );
        // });

        this.currentProduct = this.products[this.currentIndex];
        this.productAvailable = true;
        this.isLoading = false;
      } catch (error) {
        console.error('Error fetching products:', error);
        this.isLoading = false;
        this.productAvailable = false;
      }
    },
    nextProduct() {
      this.currentIndex = (this.currentIndex + 1) % this.products.length;
      this.currentProduct = this.products[this.currentIndex];
      if (this.currentProductClass === 'unavailable-product') {
        this.productAvailable = false;
      } else {
        return (this.productAvailable = true);
      }
    },
  },
};
</script>

<!-- Add "scoped" attribute to limit CSS to this component only -->
<style>
:root {
  --baby-blue: #d6e6ff;
  --blue: #002772;
  --grey: #dcdcdc;
  --magenta: #720060;
  --pink: #fde2ff;
  --soft-dark: #1e1e1e;
}

.men-section {
  background-color: var(--baby-blue);
  color: var(--blue);
}

.men-section button {
  background-color: var(--blue);
  border: 2px solid var(--blue);
  color: #fff;
}

.men-section button:last-of-type {
  background-color: #fff;
  color: var(--blue);
}

.women-section {
  background-color: var(--pink);
  color: var(--magenta);
}

.women-section button {
  background-color: var(--magenta);
  border: 2px solid var(--magenta);
  color: #fff;
}

.women-section button:last-of-type {
  background-color: #fff;
  color: var(--magenta);
}

.unavailable-product {
  background-color: var(--grey);
}
.home-page {
  display: flex;
  flex-wrap: wrap;
  justify-content: center;
  text-align: left;
  padding: 0;
  margin: 0;
  height: 70vh;
}

.unavailable {
  display: flex;
  flex-direction: column;
  margin-top: 10vh;
  justify-content: center;
  align-items: center;
  height: 80vh;
  width: 70%;
  border: 1px solid #ccc;
  background-color: #fff;
  box-shadow: 2px 5px 10px 2px #888888;
}

.image {
  padding: 100px;
  display: block;
  max-height: 300px;
  max-width: 200px;
  object-fit: contain;
}

.product {
  display: flex;
  margin-top: 10vh;
  justify-content: center;
  align-items: center;
  height: 80vh;
  width: 70%;
  border: 1px solid #ccc;
  background-color: #fff;
  box-shadow: 2px 5px 10px 2px #888888;
}

.description {
  width: 400px;
  height: 400px;
  margin: 60px;
}

.description h1 {
  font-size: larger;
  margin-bottom: 20px;
  height: 50px;
}

.description h2 {
  font-size: large;
  margin-bottom: 10px;
  color: var(--soft-dark);
}

.description h3 {
  margin: 10px 0 10px 0;
}

.description p {
  margin: 20px 0 20px 0;
  overflow-y: scroll;
  font-size: small;
  height: 30%;
  color: var(--soft-dark);
}

.description button {
  padding: 10px 0 10px 0;
  width: 9.5em;
  border-radius: 5px;
}

.description button:first-of-type {
  margin-right: 10em;
}

.unavailable button {
  padding: 5px 100px 5px 100px;
  margin-top: 10px;
  background-color: #fff;
}

@media only screen and (max-width: 1200px) {
  .description h1 {
    font-size: medium;
  }

  .description button {
    display: block;
    width: 100%;
    padding: 20px;
  }
  .description button:first-of-type {
    margin: 0 0 10px 0;
  }
}
</style>
