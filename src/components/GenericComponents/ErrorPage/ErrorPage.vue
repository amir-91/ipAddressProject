<template>
  <div class="error-page">
    <div><img src="../../../assets/images/something-went-wrong.svg" /></div>
    <div><p>Something went wrong, please try again</p></div>
    <div><a @click="reloadPage">Reload</a></div>
  </div>
</template>

<script>
export default {
  methods: {
    reloadPage () {
      window.location.reload()
    }
  }
}
</script>
