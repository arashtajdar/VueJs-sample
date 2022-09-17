<template>
  <div>
    <h1>Category list</h1>
    <div class="container">
      <div class="row">
        <div class="col-1">
        </div>
        <div class="col-10">
            <div v-if="loadingCategories" class="spinner-border text-success" role="status">
              <span class="sr-only"></span>
            </div>
            <table v-if="!loadingCategories" class="table table-striped">
              <thead>
              <tr>
                <th scope="col">#</th>
                <th scope="col">ID</th>
                <th scope="col">Name</th>
                <th scope="col">Actions</th>
              </tr>
              </thead>
              <tbody>
              <tr v-for="(category,k) in categories.list" :key="category.category_id" >
                <th scope="row">{{ k+1 }}</th>
                <td>{{ category.category_id }}</td>
                <td>{{ category.category_name }}</td>
                <td><span class="deleteBtn" @click="removeCategory(category.category_id)">X</span></td>
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
  name: "CategoryList",
  components: {
    VueBasicAlert
  },
  data() {
    return {
      loadingCategories:true,
      posts: {
        category_id: null,
        category_name: null,
        creation_date: null,
      },
      categories: {
        list: [
          {
            "category_id" : null,
            "category_name" : null,
            "creation_date" : null,
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

    getCategories() {
      let vm = this;
      vm.loadingCategories = true;

      axios
          .request({
            url: process.env.VUE_APP_BASEURL+'category',
            method: 'get',
            headers: {
              'Authorization': 'Bearer '+process.env.VUE_APP_TOKEN
            }
          })
          .then(response => {
            console.log(response.data);
            vm.categories.list = response.data;
            vm.loadingCategories = false;
          })
    },
    removeCategory(id){
      let vm = this;
      if(confirm("Do you really want to delete?")){
        vm.loadingCategories = true;
        axios
            .request({
              url: process.env.VUE_APP_BASEURL+'category/'+id,
              method: 'delete',
              headers: {
                'Authorization': 'Bearer '+process.env.VUE_APP_TOKEN
              }
            })
            .then(response => {
              vm.$refs.alert.showAlert(
                  'Success',
                  "category deleted successfully!",
                  'Success',
                  "Success",
                  'Success'
              );
              console.log(response.data);
              vm.getCategories();
            })
      }

    }
  },
  mounted() {
    this.getCategories();
    this.$root.eventEmitter.on('reload-category-list', () => {
      this.getCategories();
    });
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