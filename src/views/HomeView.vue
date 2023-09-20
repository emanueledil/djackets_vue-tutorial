<template>
  <div class="home">
    home
  </div>
  <div class="column is-multiline">
    <div class="column is-12">
      <h2 class="is-size-2 has-text-centered">Latest products</h2>
    </div>
    <ProductBox 
    v-for="product in latestProducts"
    v-bind:key="product.id"
    v-bind:product="product" />
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

import axios from 'axios'
import ProductBox from '@/components/ProductBox.vue'

export default{
  name: 'home',
  data(){
    return {
      latestProducts: [],
      showMobileMenu: false
    } 
  },
  components:{
    ProductBox
  },
  mounted(){
    this.getLatestProducts()
  },
  methods:{
    getLatestProducts(){
      axios.
      get('/api/v1/latest-products/').
      then(response=>{
        this.latestProducts= response.data
      }).catch(error=>{
        console.log(error)
      })
    }
  }
}
</script>
