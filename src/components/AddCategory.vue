<template>
  <h1>Add new Category</h1>
  <form @submit="PostData" method="post">
    <input class="st-input" type="text" name="name" placeholder="Category name" v-model="category.name"> <br><br>
    <button type="submit">CREATE</button>
  </form>
  <vue-basic-alert ref="alert" :duration="500" :closeIn="3000"/>

</template>

<script>
import axios from "axios";
import VueBasicAlert from "vue-basic-alert";
export default {
  name: "AddCategory",
  components: {
    VueBasicAlert
  },
  data(){
    return {
      category:{
        name:null
      }
    }
  },
  methods:{
    PostData(e){
      let vm = this;
      axios
          .request({
            url: process.env.VUE_APP_BASEURL+'category',
            method: 'post',
            data: this.category,
            headers: {
              'Authorization': 'Bearer '+process.env.VUE_APP_TOKEN
            }
          })
          .then(response => {
            console.log(response);
            vm.$refs.alert.showAlert(
                'Success',
                "Category created successfully!",
                'Success',
                "Success",
                'Success'
            );
          })
      e.preventDefault();
    }
  },
}
</script>

<style scoped>
</style>