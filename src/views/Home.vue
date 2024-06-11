<template>
  <div class="container my-5 text-center">
    <h5>Welcome, {{ userName }}</h5>
  </div>
</template>
<script>
export default {
  data() {
    return {
      userName: ''
    }
  },
  mounted() {
    this.userName = localStorage.getItem('userName');
  }
}
</script>
