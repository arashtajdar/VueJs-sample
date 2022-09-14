<template>
  <h1>Add new Category</h1>
  <form @submit="PostData" method="post">
    <input class="st-input" type="text" name="name" placeholder="Category name" v-model="category.name"> <br><br>
    <button type="submit">Add new author</button>
  </form>
  <vue-basic-alert ref="alert" :duration="500" :closeIn="3000"/>

</template>

<script>
// import axios from "axios";
import VueBasicAlert from "vue-basic-alert";
export default {
  name: "AddCategory",
  components: {
    VueBasicAlert
  },
  data(){
    return {
      category:{
        name:null,
      }
    }
  },
}
</script>

<style scoped>
</style>