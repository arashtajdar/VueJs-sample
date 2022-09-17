<template>
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <button class="navbar-toggler" type="button" data-toggle="collapse" data-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item" :class="{ active: current === 'HomePage' }">
          <a class="nav-link" @click="current= 'HomePage'" href="#">Home</a>
        </li>
        <li class="nav-item" :class="{ active: current === 'Product' }">
          <a class="nav-link" @click="current= 'Product'" href="#">Product</a>
        </li>
        <li class="nav-item" :class="{ active: current === 'Category' }">
          <a class="nav-link" @click="current= 'Category'" href="#">Category</a>
        </li>
      </ul>
    </div>
  </nav>
  <HomePage v-if="current==='HomePage'"/>
  <Category v-if="current==='Category'"/>
  <Product v-if="current==='Product'"/>
  <Footer/>
</template>

<script>
import Category from './components/Category.vue'
import Product from './components/Product.vue'
import HomePage from './components/HomePage.vue'
import Footer from './components/Footer.vue'
import mitt from 'mitt';
const eventEmmiter = mitt();
export default {
  name: 'App',
  components: {
    Category,HomePage,Product,Footer
  },
  data(){
    return {
      current: "HomePage",
      eventEmitter: eventEmmiter,
      test: "111"
    }
  },
  methods: {

  },mounted() {
    eventEmmiter.on('my-event', (evt) => {
      console.log(evt);
      console.log("yeeeeeeeeees");
    })
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
.nav-item {
  display: inline;
  margin-right: 3%;
  padding: 5px;
  border: 1px solid #41b883;
  background: white;
}
.nav-item.active{
  background: #41b883;
}
.nav-item.active>.nav-link{
  color:white;
}
.nav-link {
  text-decoration: navajowhite;
  color: black;
  font-size: 16px;
}
.nav-link:hover {
  color: #41b883;
}
</style>
Footer
