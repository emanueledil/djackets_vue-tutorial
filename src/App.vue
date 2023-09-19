
import router from './router';
<template>
  <nav class="navbar is-dark">
    <div class="navbar-brand">
      <router-link to="/" class="navbar-item"><strong>Djackets</strong></router-link>

      <a class="navbar-burger" aria-label="menu" aria-expanded="false" data-target="navbar-menu" @click="showMobileMenu = !showMobileMenu">
        <span aria-hidden="true"></span>
        <span aria-hidden="true"></span>
   
      </a>
    </div>

    <div class="navbar-menu" id="navbar-menu" v-bind:class="{'is-active': showMobileMenu }">
      <div class="navbar-start">
        <div class="navbar-item">
          <form method="get" action="/search">
            <div class="field has-addons">
              <div class="control">
                <input type="text" class="input" placeholder="What are you looking for?" name="query">
              </div>

              <div class="control">
                <button class="button is-success">
                    <span class="icon">
                    <i class="fas fa-search"></i>
                    </span>
                </button>
              </div>
            </div>
          </form>
        </div>
      </div>

      <div class="navbar-end">
        <router-link to="/summer" class="navbar-item">Summer</router-link>
        <router-link to="/winter" class="navbar-item">Winter</router-link>

        <div class="navbar-item">
          <div class="buttons">
            <template v-if="$store.state.isAuthenticated">
              <router-link to="/my-account" class="button is-light">My account</router-link>
            </template>

            <template v-else>
              <router-link to="/log-in" class="button is-light">Log in</router-link>
            </template>

            <router-link to="/cart" class="button is-success">
              <span class="icon"><i class="fas fa-shopping-cart"></i></span>
              <span>Cart ({{ cartTotalLength }})</span>
            </router-link>
          </div>
        </div>
      </div>
    </div>
  </nav>



  <section class="section">
    <router-view/>
  </section>

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
        view details
      </div>
    </div> 
  </div>

  <footer class="footer">
    <p class="has-text-centered">Djackets</p>
  </footer>
</template>

<script>
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

<style lang="scss">
@import '../node_modules/bulma/';
.image{
  margin-top: -1.25rem;
  margin-left: -1.25rem;
  margin-right: -1.25rem;
}
</style>
