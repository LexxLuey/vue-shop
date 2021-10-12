<template>
  <div>
    <main class="wrapper">
      <h1>Products</h1>

      <div class="card-container">
        <ProductCard
          v-for="(product, index) in inventory"
          :key="product.id"
          :index="index"
          :product="product"
          :addToCart="addToCart"
          class="card"
        />

      </div>
    </main>
  </div>
</template>

<script>
import ProductCard from '@/components/ProductCard.vue'
// @ is an alias to /src
// import HelloWorld from '@/components/HelloWorld.vue'

export default {
  name: 'Products',
  props: ['inventory', 'addToCart'],

  methods: {

  },
  components: {
    ProductCard
  }
}
</script>
