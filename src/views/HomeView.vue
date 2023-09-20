<template>
  <div class="home">
    home
  </div>
  <div class="column is-multiline">
    <div class="column is-12">
      <h2 class="is-size-2 has-text-centered">Latest products</h2>
    </div>
    <div class="column is-3" 
      v-for="product in latestProducts"
      v-bind:key="product.id"
      >
      <div class="box">
        <figure class="image mb-4">
          <img v-bind:src="product.get_thumbnail">
        </figure>
        <h3 class="is-size-4">{{product.name}}</h3>
        <p class="is-size-6 has-text-grey"> {{product.price}} EUR</p>
      
        <router-link v-bind:to="product.get_absolute_url" class="button is-dark mt-4">View details </router-link>
      </div>
    </div> 
  </div>
</template>

<script>
// @ is an alias to /src
import HelloWorld from '@/components/HelloWorld.vue'

import axios from 'axios'

export default{
  name: 'home',
  data(){
    return {
      latestProducts: [],
      showMobileMenu: false
    } 
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
