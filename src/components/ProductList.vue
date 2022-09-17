<template>
  <div>
    <h1>Product list</h1>
    <div class="container">
      <div class="row">
        <div class="col-1">
        </div>
        <div class="col-10">
            <div v-if="loadingProducts" class="spinner-border text-success" role="status">
              <span class="sr-only"></span>
            </div>
            <table v-if="!loadingProducts" class="table table-striped">
              <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">Code</th>
                <th scope="col">Title</th>
                <th scope="col">Description</th>
                <th scope="col">Category</th>
                <th scope="col">Actions</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="(product,k) in products.list" :key="product.product_code" >
                <th scope="row">{{ k+1 }}</th>
                <td>{{ product.product_code }}</td>
                <td>{{ product.product_title }}</td>
                <td>{{ product.product_category_name }}</td>
                <td>{{ product.product_description }}</td>
                <td><span class="deleteBtn" @click="removeProduct(product.product_id)">X</span></td>
              </tr>
              </tbody>
            </table>
        </div>
        <div class="col-1">
        </div>
      </div>
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
        product_id: null,
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
    },
    removeProduct(id){
      let vm = this;
      if(confirm("Do you really want to delete?")){
        vm.loadingProducts = true;
        axios
            .request({
              url: process.env.VUE_APP_BASEURL+'products/'+id,
              method: 'delete',
              headers: {
                'Authorization': 'Bearer '+process.env.VUE_APP_TOKEN
              }
            })
            .then(response => {
              vm.$refs.alert.showAlert(
                  'Success',
                  "product deleted successfully!",
                  'Success',
                  "Success",
                  'Success'
              );
              console.log(response.data);
              vm.getProducts();
            })
      }

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
.deleteBtn{
  color: red;
  cursor: pointer;
}
</style>