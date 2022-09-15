<template>
  <img alt="Vue logo" style="width: 100px;" src="./assets/logo.png">
  <nav class="navbar navbar-expand-lg navbar-light bg-light">
    <div class="collapse navbar-collapse" id="navbarNav">
      <ul class="navbar-nav">
        <li class="nav-item" :class="{ active: current === 'HomePage' }">
          <a class="nav-link" @click="current= 'HomePage'" href="#">Home</a>
        </li>
        <li class="nav-item" :class="{ active: current === 'AddProduct' }">
          <a class="nav-link" @click="current= 'AddProduct'" href="#">Add Product</a>
        </li>
        <li class="nav-item" :class="{ active: current === 'AddCategory' }">
          <a class="nav-link" @click="current= 'AddCategory'" href="#">Add Category</a>
        </li>
      </ul>
    </div>
  </nav>
  <HomePage v-if="current==='HomePage'"/>
  <AddCategory v-if="current==='AddCategory'"/>
  <AddProduct v-if="current==='AddProduct'"/>
</template>

<script>
import AddCategory from './components/AddCategory.vue'
import AddProduct from './components/AddProduct.vue'
import HomePage from './components/HomePage.vue'
export default {
  name: 'App',
  components: {
    AddCategory,HomePage,AddProduct
  },
  data(){
    return {
      current: "HomePage",
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
  margin-top: 60px;
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
