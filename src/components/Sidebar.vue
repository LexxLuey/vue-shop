<template>
  <div>
    <aside class="cart-container">
      <div class="cart">
        <h1 class="cart-title spread">
         <span>
          Cart
          <i class="icofont-cart-alt icofont-1x" />
         </span>
         <button @click="toggle" class="cart-close">&times;</button>
        </h1>

        <div class="cart-body">
          <table class="cart-table">
            <thead>
              <tr>
                <th><span class="sr-only">Product Image</span></th>
                <th>Product</th>
                <th>Price</th>
                <th>Qty</th>
                <th>Total</th>
              </tr>
            </thead>
            <tbody>
              <tr v-for="(quantity, key, i) in cart" :key="i">
                <td><i class="icofont-carrot icofont-3x"/></td>
                <td> {{key}} </td>
                <td> N{{getPrice(key)}} </td>
                <td class="center"> {{quantity}} </td>
                <td> N{{quantity * getPrice(key)}} </td>
                <td class="center">
                  <button @click="remove(key)" class="btn btn-light cart-remove">&times;</button>
                </td>
              </tr>
            </tbody>
          </table>

          <p class="center" v-if="!Object.keys(cart).length"><em>No items in cart</em></p>
          <div class="spread">
            <span><strong>Total:</strong> N{{calculateTotal()}} </span>
            <button class="btn btn-light">Checkout</button>
          </div>
        </div>
      </div>
    </aside>
  </div>
</template>

<script>
export default {
  props: ['toggle', 'cart', 'inventory', 'remove'],

  methods: {
    getPrice (name) {
      const product = this.inventory.find((p) => {
        return p.name === name
      })
      console.log('see cart: ', this.cart)
      console.log('see inventory: ', this.inventory)
      return product.price.USD
    },
    calculateTotal () {
      const total = Object.entries(this.cart).reduce((acc, curr, index) => {
        return acc + (curr[1] * this.getPrice(curr[0]))
      }, 0)
      return total.toFixed(2)
    }
  }
}
</script>
