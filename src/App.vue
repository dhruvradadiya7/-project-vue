<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="container px-4 px-lg-5">
      <a class="navbar-brand" href="#">Softhub</a>
      <button
        class="navbar-toggler"
        type="button"
        data-bs-toggle="collapse"
        data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent"
        aria-expanded="false"
        aria-label="Toggle navigation"
      >
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0 ms-lg-4">
          <li class="nav-item">
            <router-link class="nav-link active" aria-current="page" to="/"
              >Home</router-link
            >
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/about">About</router-link>
          </li>
          <li class="nav-item">
            <router-link class="nav-link" to="/product-add"
              >Product Add</router-link
            >
          </li>
        </ul>
        <form class="d-flex">
          <button
            class="btn btn-outline-dark"
            type="button"
            @click="toggleSideBar"
          >
            <i class="bi-cart-fill me-1"></i>
            Cart
            <span class="badge bg-dark text-white ms-1 rounded-pill">
              {{ totalQuantity }}</span
            >
          </button>
        </form>
      </div>
    </div>
  </nav>
  <!-- Header-->
  <header class="backimage py-5">
    <div class="container px-4 px-lg-5 my-5">
      <div class="text-center text-white">
        <h1 class="display-4 fw-bolder">Shop with Softhub</h1>
        <p class="lead fw-normal text-white-50 mb-0">
          Popular apps with huge discounts.
        </p>
      </div>
    </div>
  </header>
  <router-view
  :inventory = "inventory"
  :addToCart = "addToCart"
  />
<Sidebar
  v-if="showSideBar"
  :toggle="toggleSideBar"
  :cart = "cart"
  :inventory = "inventory"
  :remove = "removeItem"
  />
</template>
<script>
import product from '@/product.json'
import Sidebar from '@/components/SideBar.vue'
export default {
  components: {
    Sidebar
  },
  data () {
    return {
      showSideBar: false,
      inventory: product,
      cart: {}
    }
  },
  methods: {
    toggleSideBar () {
      this.showSideBar = !this.showSideBar
    },
    addToCart (name, index) {
      if (!this.cart[name]) this.cart[name] = 0
      this.cart[name] += this.inventory[index].quantity
      console.log(this.cart[name])
    },
    removeItem (name) {
      delete this.cart[name]
    }
  },
  computed: {
    totalQuantity () {
      return Object.values(this.cart).reduce((acc, curr) => {
        return acc + curr
      }, 0)
    }
  }
}
</script>
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
