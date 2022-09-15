<template>
  <div>
    <h1>Product list</h1>
    <div>
      <h4 v-if="loadingProducts">Loading product list</h4>
      <table v-if="!loadingProducts" class="table">
        <thead>
        <tr>
          <th scope="col">#</th>
          <th scope="col">Code</th>
          <th scope="col">Title</th>
          <th scope="col">Description</th>
          <th scope="col">Category</th>
        </tr>
        </thead>
        <tbody>
        <tr v-for="(product,k) in products.list" :key="product.product_code" >
          <th scope="row">{{ k+1 }}</th>
          <td>{{ product.product_code }}</td>
          <td>{{ product.product_title }}</td>
          <td>{{ product.product_category_name }}</td>
          <td>{{ product.product_description }}</td>
        </tr>
        </tbody>
      </table>
    </div>

    <vue-basic-alert ref="alert" :duration="500" :closeIn="3000"/>
  </div>
</template>

<script>

import axios from "axios";
import VueBasicAlert from "vue-basic-alert";

export default {
  name: "ProductList",
  components: {
    VueBasicAlert
  },
  data() {
    return {
      loadingProducts:true,
      posts: {
        code: null,
        title: null,
        description: null,
        category_id: null
      },
      products: {
        list: [
          {
            "product_code" : null,
            "product_title" : null,
            "product_category_name" : null,
            "product_description" : null,
          }
        ],
        selected: '',
        prefix: '',
        first: '',
        last: ''
      }
    }
  },
  methods: {

    getProducts() {
      let vm = this;
      axios
          .request({
            url: process.env.VUE_APP_BASEURL+'products',
            method: 'get',
            headers: {
              'Authorization': 'Bearer '+process.env.VUE_APP_TOKEN
            }
          })
          .then(response => {
            console.log(response.data);
            vm.products.list = response.data;
            vm.loadingProducts = false;
          })
    }
  },
  mounted() {
    this.getProducts();
    },
}
</script>

<style scoped>
table{
  margin: auto;
}
</style>