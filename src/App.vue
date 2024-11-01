<template>
  <div id="app">
    <header class="header">
      <h1 class="logo">VueShop</h1>
      <div class="cart-icon" @click="toggleCart">
        🛒
        <span v-if="cartItemCount">{{ cartItemCount }}</span>
      </div>
    </header>
    <router-view :cart="cart" :add-to-cart="addToCart" />
    <div class="cart-sidebar" :class="{ 'cart-sidebar--active': isCartOpen }">
      <h2>Cart</h2>
      <ul v-if="cart.length">
        <li v-for="item in cart" :key="item.id">
          {{ item.name }} x {{ item.quantity }} - ${{
            (item.price * item.quantity).toFixed(2)
          }}
          <button @click="removeFromCart(item)">Remove</button>
        </li>
      </ul>
      <p v-if="cart.length">Total: ${{ cartTotal }}</p>
      <p v-else>Your cart is empty</p>
      <button @click="toggleCart" class="close-cart">Close Cart</button>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      isCartOpen: false,
      cart: [],
    }
  },
  computed: {
    cartItemCount() {
      return this.cart.reduce((total, item) => total + item.quantity, 0)
    },
    cartTotal() {
      return this.cart
        .reduce((total, item) => total + item.price * item.quantity, 0)
        .toFixed(2)
    },
  },
  methods: {
    toggleCart() {
      this.isCartOpen = !this.isCartOpen
    },
    addToCart(product) {
      const existingItem = this.cart.find((item) => item.id === product.id)
      if (existingItem) {
        existingItem.quantity += 1
      } else {
        this.cart.push({ ...product, quantity: 1 })
      }
    },
    removeFromCart(item) {
      const index = this.cart.findIndex((i) => i.id === item.id)
      if (index !== -1) {
        if (this.cart[index].quantity > 1) {
          this.cart[index].quantity -= 1
        } else {
          this.cart.splice(index, 1)
        }
      }
    },
  },
}
</script>

<style>
/* General styling for the app */
* {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
}

body {
  font-family: Arial, sans-serif;
  background: url("https://via.placeholder.com/1600x900") no-repeat center
    center fixed;
  background-size: cover;
  color: #333;
}

a {
  color: #42b983;
  text-decoration: none;
}

a:hover {
  text-decoration: underline;
}

#app {
  display: flex;
  flex-direction: column;
  align-items: center;
}

/* Header Styling */
.header {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 10px 20px;
  background: rgba(255, 255, 255, 0.8);
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.2);
  position: fixed;
  width: 100%;
  top: 0;
  z-index: 10;
}

.logo {
  font-size: 1.5rem;
  font-weight: bold;
}

.cart-icon {
  cursor: pointer;
  font-size: 1.5rem;
  position: relative;
}

.cart-icon span {
  position: absolute;
  top: -5px;
  right: -10px;
  background: #42b983;
  color: white;
  padding: 2px 5px;
  border-radius: 50%;
  font-size: 0.8rem;
}

/* Cart Sidebar Styling */
.cart-sidebar {
  position: fixed;
  right: 0;
  top: 0;
  width: 300px;
  height: 100%;
  background: white;
  padding: 20px;
  box-shadow: -2px 0 5px rgba(0, 0, 0, 0.2);
  transform: translateX(100%);
  transition: transform 0.3s ease-in-out;
  overflow-y: auto;
  z-index: 20;
}

.cart-sidebar--active {
  transform: translateX(0);
}

.cart-sidebar h2 {
  font-size: 1.3rem;
  margin-bottom: 20px;
}

.cart-sidebar button {
  background: #42b983;
  color: white;
  border: none;
  padding: 10px;
  border-radius: 4px;
  cursor: pointer;
}

.cart-sidebar .close-cart {
  background: #e74c3c;
  margin-top: 20px;
}
</style>
