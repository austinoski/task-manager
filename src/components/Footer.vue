<template>
    <footer>
        <p>Copyright &copy; 2022</p>
        <div v-show="this.$route.path === '/'">
            <router-link to="/about">About</router-link>
        </div>
    </footer>
</template>

<script>
export default {
    name: "Footer"
}
</script>

<style scoped>
  a {
      color: #333
  }
  footer {
      margin-top: 30px;
      text-align: center;
  }
  .footer-links {
      text-decoration: none;
  }
</style>
