<template>
  <div id="login">
    <div class="left-side">
    </div>
    <div class="right-side">
      <div class="form">
        <h1>Sign Up</h1>
        <input-field name="email" placeholder="Your email"></input-field>
        <input-field name="password" placeholder="Your password" type="password"></input-field>
        <button-primary text="Sign up" type="submit"></button-primary>
        <span class="choice">Already a member? <router-link to="login">Login </router-link> instead!</span>
      </div>
    </div>
  </div>
</template>

<script lang="ts">
import { defineComponent } from 'vue';
import InputField from "@/components/InputField.vue";
import ButtonPrimary from "@/components/Button.vue";

export default defineComponent({
  name: 'SignUpView',
  components: {ButtonPrimary, InputField},
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
  .right-side {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .form {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    padding: 60px;
    border-style: solid;
    border-width: 1px;
    border-color: rgba(210, 210, 213, 0.5);
    background-color: #fff;
    width: 80%;
    .choice {
      font-size: 16px;
      line-height: 30px;
      text-align: center;
    }
  }
}
</style>