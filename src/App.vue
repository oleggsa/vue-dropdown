<template>
  <Dropdown />
</template>

<script>
import Dropdown from "@/components/Dropdown";

export default {
  name: 'App',
  components: {
    Dropdown
  }
}
</script>

<style lang="scss">
body {
  box-sizing: border-box;
  margin: 0;
  padding: 0;
  height: 600px;
}
*, *::before, *::after {
  box-sizing: border-box;
}
#app {
  display: flex;
  justify-content: center;
  align-items: center;
  min-height: 20vh;
}
</style>
