// Menu.vue
<template>
  <div>
    <h2>Menu</h2>
    <div v-for="item in menu" :key="item.id">
      <p>{{ item.name }} - ${{ item.price }}</p>
      <button @click="addToCart(item)">Add to Cart</button>
    </div>
  </div>
</template>

<script>
import axios from 'axios';

export default {
  data() {
    return {
      menu: [],
      cart: [],
    };
  },
  mounted() {
    this.fetchMenu();
  },
  methods: {
    fetchMenu() {
      axios.get('http://localhost:3000/menu')
        .then(response => {
          this.menu = response.data;
        })
        .catch(error => {
          console.error('Error fetching menu:', error);
        });
    },
    addToCart(item) {
      this.cart.push(item);
    },
  },
};
</script>
