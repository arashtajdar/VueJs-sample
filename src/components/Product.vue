<template>
  <ProductList />
  <AddProduct />
</template>

<script>
import AddProduct from './AddProduct.vue'
import ProductList from './ProductList.vue'
export default {
  name: 'App',
  components: {
    ProductList,AddProduct
  },
  data(){
    return {
    }
  }
}
</script>

<style scoped>

</style>