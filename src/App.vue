<template>
  <div class="container">
    <the-form></the-form>
  </div>
</template>

<script>
import TheForm from './components/TheForm.vue';

export default {
  components: {
    TheForm
  }  
}
</script>

<style>
@import url('https://cdn.jsdelivr.net/npm/bootstrap@5.1.3/dist/css/bootstrap.min.css');
npm
* {
  box-sizing: border-box;
}

html {
  font-family: sans-serif;
}

body {
  margin: 0;
  background-color: #292929;
}
</style>