<template>
  <v-app>
    <v-main>
      <IndexPage/>
    </v-main>
  </v-app>
</template>

<script>
import IndexPage from './pages/IndexPage';

export default {
  name: 'App',
  components: {
    IndexPage,
  }
};
</script>

<style lang="scss">
@import "styles/index.scss";
</style>
