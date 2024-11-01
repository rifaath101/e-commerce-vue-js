<template>
  <div class="shop-page">
    <h2>Shop</h2>
    <div class="product" v-for="product in products" :key="product.id">
      <h3>{{ product.name }}</h3>
      <p>{{ product.description }}</p>
      <p>${{ product.price }}</p>
      <button @click="addToCart(product)">Add to Cart</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      products: [
        {
          id: 1,
          name: "Product 1",
          description: "Description for product 1",
          price: 10.99,
        },
        {
          id: 2,
          name: "Product 2",
          description: "Description for product 2",
          price: 15.99,
        },
        {
          id: 3,
          name: "Product 3",
          description: "Description for product 3",
          price: 8.99,
        },
      ],
      cart: [],
    }
  },
  methods: {
    addToCart(product) {
      this.cart.push(product)
      alert(`${product.name} added to cart!`)
    },
  },
}
</script>

<style scoped>
.shop-page {
  max-width: 800px;
  margin: 50px auto;
  text-align: center;
}

.product {
  border: 1px solid #ddd;
  border-radius: 8px;
  padding: 20px;
  margin: 20px 0;
  box-shadow: 0 4px 8px rgba(0, 0, 0, 0.1);
  transition: transform 0.2s;
}

.product:hover {
  transform: translateY(-5px);
}

.product h3 {
  font-size: 1.5rem;
  color: #333;
}

.product p {
  color: #666;
  font-size: 1rem;
  margin: 5px 0;
}

button {
  padding: 10px 20px;
  background-color: #42b983;
  color: white;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  transition: background-color 0.3s;
}

button:hover {
  background-color: #379170;
}
</style>
