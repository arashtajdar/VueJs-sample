<template>
  <div>
    <h1>Create new product</h1>
    <form @submit="PostData" method="post">
      <input class="st-input form-control" type="text" name="code" placeholder="product code" v-model="posts.code"> <br><br>
      <input class="st-input form-control" type="text" name="title" placeholder="product title" v-model="posts.title"> <br><br>
      <input class="st-input form-control" type="text" name="description" placeholder="product description" v-model="posts.description"> <br><br>
      <input class="st-input form-control" v-model="categories.prefix" placeholder="Type category name to search"><br>
      <select v-show="categories.prefix.length > 2" class="st-input form-control" name="category" size="5"
              v-model="posts.category_id">
        <option v-for="category in filteredNames" :key="category.category_id" :value="category.category_id">
          {{ category.category_name }}
        </option>
      </select> <br><br>
      <button type="submit" class="btn btn-outline-success">Create product</button>
    </form>
    <vue-basic-alert ref="alert" :duration="500" :closeIn="3000"/>
  </div>
</template>

<script>

import axios from "axios";
import VueBasicAlert from "vue-basic-alert";

export default {
  name: "AddProduct",
  components: {
    VueBasicAlert
  },
  data() {
    return {
      posts: {
        code: null,
        title: null,
        description: null,
        category_id: null
      },
      categories: {
        names: [
          {
            "category_id": 1,
            "category_name": "Phyllis Zulauf IV",
            "Creation_date": "2022-04-16T11:50:47.000000Z"
          }
        ],
        selected: '',
        prefix: '',
        first: '',
        last: ''
      }
    }
  },
  computed: {
    filteredNames() {
      console.log('comuted');

      return this.categories.names.filter((n) =>
          n.category_name.toLowerCase().search(this.categories.prefix.toLowerCase()) >= 0
      )
    }
  },
  methods: {
    PostData(e) {
      let vm = this;
      axios
          .request({
            url: process.env.VUE_APP_BASEURL+'products',
            method: 'post',
            data: this.posts,
            headers: {
              'Authorization': 'Bearer '+process.env.VUE_APP_TOKEN
            }
          })
          .then(response => {
            console.log(response);
            vm.$refs.alert.showAlert(
                'Success',
                "Book added successfully!",
                'Success',
                "Success",
                'Success'
            );
            vm.posts.code = null;
            vm.posts.title = null;
            vm.posts.description = null;
            vm.posts.category_id = null;
            vm.categories.prefix = '';
          })
      e.preventDefault();
    },
    getCategories() {
      let vm = this;
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
            vm.categories.names = response.data;
          })
    }
  },
  mounted() {
    this.getCategories();
  },
}
</script>

<style scoped>
.st-input {
  min-width: 200px;
}
</style>