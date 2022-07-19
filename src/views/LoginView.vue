<template>
  <div id="login">
    <div class="left-side">
    </div>
    <div class="right-side">
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';

export default defineComponent({
  name: 'HomeView',
});
</script>


<style lang="scss" scoped>
#login {
  width: 100%;
  height: 100vh;
  display: flex;
  flex-direction: row;
  .left-side, .right-side {
    width: 50%;
    height: 100vh;
  }
  .left-side {
    background-image: url('~@/assets/coffee-background.jpg');
    background-position: center;
    background-size: cover;
  }
}
</style>