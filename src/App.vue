<template>
  <n-config-provider :theme="darkTheme">
    <div id="nav">
      <router-link to="/">Home</router-link> |
      <router-link to="/about">About</router-link>
    </div>
    <router-view />
  </n-config-provider>
</template>

<script>
import { defineComponent } from "vue";
import { darkTheme, NConfigProvider } from "naive-ui";

export default defineComponent({
  components: {
    NConfigProvider,
  },
  setup() {
    return {
      darkTheme,
    };
  },
});
</script>

<style lang="scss">
html {
  background: #090c0f;
}

#nav {
  padding: 30px;
  text-align: center;

  a {
    font-weight: bold;
    color: #7089a0;

    &.router-link-exact-active {
      color: #42b983;
    }
  }
}
</style>
