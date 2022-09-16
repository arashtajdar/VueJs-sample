<template>
  <CategoryList />
  <AddCategory />
</template>

<script>
import CategoryList from './CategoryList.vue'
import AddCategory from "@/components/AddCategory";
export default {
  name: 'App',
  components: {
    CategoryList,AddCategory
  },
  data(){
    return {
    }
  }
}
</script>

<style scoped>

</style>