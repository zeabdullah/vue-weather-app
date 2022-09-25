<template>
  <header id="header">
    <h1>Weather App</h1>
  </header>
</template>

<script>
export default {
  name: 'Header'
};
</script>

<style lang="scss" scoped>
#header {
  margin-bottom: 1em;

  h1 {
    display: flex;
    align-items: center;
    justify-content: center;

    padding: 0.5em 0;
    font-size: 1.5em;
    font-weight: Bold;
    color: rgb(0, 0, 0);
    background: #ffffff;
  }
}
</style>
