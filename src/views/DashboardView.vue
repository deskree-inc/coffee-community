<template>
  <div class="dashboard-wrapper">
    <div class="my-products-nav">
      <button-primary text="New Product" @click="newProduct"></button-primary>
    </div>
    <div class="my-products">
    </div>
  </div>
</template>

<script lang="ts">
import {defineComponent} from 'vue';
import ButtonPrimary from "@/components/Button.vue";

export default defineComponent({
  name: 'DashboardView',
  components: {ButtonPrimary},
  methods: {
    newProduct() {
      console.log("newProduct");
    }
  }
});
</script>

<style scoped>
.dashboard-wrapper {
  padding: 100px 10%;
}
.my-products-nav {
  width: 100%;
  display: flex;
  flex-direction: row;
  justify-content: flex-end;
}
.my-products {
  display: flex;
  margin: 0 -10px;
  -webkit-box-orient: horizontal;
  -webkit-box-direction: normal;
  flex-direction: row;
  -webkit-box-pack: center;
  justify-content: center;
  -webkit-flex-wrap: wrap;
  -ms-flex-wrap: wrap;
  flex-wrap: wrap;
  -webkit-box-align: start;
  align-items: flex-start;
  align-content: flex-start;
}
</style>