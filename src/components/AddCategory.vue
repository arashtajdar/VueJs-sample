<template>
  <div style="margin-top: 20px;" class="container">
    <div class="row">
      <div class="col">
      </div>
      <div class="col">
        <form @submit="PostData" method="post">

          <div class="input-group mb-3">
            <input
                   type="text"
                   class="form-control"
                   name="name"
                   placeholder="Category name"
                   aria-label="Category name"
                   aria-describedby="basic-addon2"
                   v-model="category.name"
            >
            <div class="input-group-append">
              <button style="border-radius: 0 10px 10px 0;" class="btn btn-outline-success" type="submit">CREATE</button>
            </div>
          </div>
        </form>
      </div>
      <div class="col">
      </div>
    </div>
  </div>

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
    emitMyEvent() {
      console.log(this.$root.eventEmitter);
      this.$root.eventEmitter.emit('reload-category-list', {})
    },
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
            this.emitMyEvent();
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