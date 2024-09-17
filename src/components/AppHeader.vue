<script>
export default {
  data() {
    return { 
      message: ' Vite-Boolflix'
    }
  }
}
</script>

<template>
  <header>
    <h1>
      {{ message }}
    </h1>
  </header>
</template>

<style lang="scss" scoped>
@use '../assets/scss/partials/variables' as *;

header {
  text-align: center;
  padding: 20px 0;
}
</style>
