<template>
  <!-- Footer -->
  <footer class="text-center text-lg-start bg-light text-muted">

    <!-- Section: Links  -->
    <section class="">
      <div class="container text-center text-md-start mt-5">
        <!-- Grid row -->
        <div class="row mt-3">
          <!-- Grid column -->
          <div class="col-md-3 col-lg-4 col-xl-3 mx-auto mb-4">
            <!-- Content -->
            <h6 class="text-uppercase fw-bold mb-4">
              <i class="fas fa-gem me-3"></i>project name
            </h6>
            <p>
              dolor sit amet, consectetur adipisicing elit.
              dolor sit amet, consectetur adipisicing elit.
              dolor sit amet, consectetur adipisicing elit.
              dolor sit amet, consectetur adipisicing elit.
            </p>
          </div>
          <!-- Grid column -->

          <!-- Grid column -->
          <div class="col-md-2 col-lg-2 col-xl-2 mx-auto mb-4">
            <!-- Links -->
            <h6 class="text-uppercase fw-bold mb-4">
              Latest Products
            </h6>
            <p v-for="(product) in products.list.reverse().slice(0,4)" :key="product.category_id" >
              {{product.product_title}}
            </p>
          </div>
          <!-- Grid column -->

          <!-- Grid column -->
          <div class="col-md-3 col-lg-2 col-xl-2 mx-auto mb-4">
            <!-- Links -->
            <h6 class="text-uppercase fw-bold mb-4">
              Latest Categories
            </h6>
            <p v-for="(category) in categories.list.reverse().slice(0,4)" :key="category.category_id" >
            {{category.category_name}}
            </p>
          </div>
          <!-- Grid column -->

          <!-- Grid column -->
          <div class="col-md-4 col-lg-3 col-xl-3 mx-auto mb-md-0 mb-4">
            <!-- Links -->
            <h6 class="text-uppercase fw-bold mb-4">Contact</h6>
            <p><i class="fas fa-home me-3"></i> Marsaskala, Malta, MSK3526</p>
            <p>
              <i class="fas fa-envelope me-3"></i>
              info@example.com
            </p>
            <p><i class="fas fa-phone me-3"></i> + 39 345 50 2629 3</p>
            <p><i class="fas fa-print me-3"></i> + 01 234 567 89</p>
          </div>
          <!-- Grid column -->
        </div>
        <!-- Grid row -->
      </div>
    </section>
    <!-- Section: Links  -->

    <!-- Copyright -->
    <div class="text-center p-4" style="background-color: rgba(0, 0, 0, 0.05);">
      © 2022 Copyright:
      <a class="text-reset fw-bold" href="https://github.com/arashtajdar">Arash Tajdar</a>
    </div>
    <!-- Copyright -->
  </footer>
  <!-- Footer -->
</template>

<script>
import axios from "axios";

export default {
  name: "FooterSection",
  data() {
    return {
    categories: {
      list: [

      ]},    products: {
      list: [

      ]}
  }},
  methods:{
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
            vm.categories.list = response.data;
          })
    },
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
            vm.products.list = response.data;
          })
    },

  },
  mounted() {
    this.getCategories();
    this.getProducts();
  }
}
</script>

<style scoped>
footer h6 {
  padding-top: 20px;
}
</style>