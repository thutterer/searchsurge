<template>
  <n-config-provider :theme="darkTheme">
    <n-space justify="space-between" align="center" id="site-header">
      <router-link to="/" id="site-title">
        <img alt="Logo" src="./assets/logo.svg" width="32" />
        <n-text>Search</n-text>
        <n-text type="success">Surge</n-text>
      </router-link>

      <nav>
        <router-link to="/">Home</router-link> |
        <router-link to="/about">About</router-link>
      </nav>
    </n-space>
    <router-view id="content-area" />
  </n-config-provider>
</template>

<script>
import { defineComponent } from "vue";
import { darkTheme, NConfigProvider, NSpace, NText } from "naive-ui";

export default defineComponent({
  components: {
    NConfigProvider,
    NSpace,
    NText,
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

#site-header {
  padding: 20px;

  #site-title {
    display: flex;
    align-items: center;
    font-size: 1.2rem;
    font-weight: bold;
    text-decoration: none;

    img {
      padding: 4px;
    }
  }

  nav {
    a {
      font-weight: bold;
      color: #e8e8e8;

      &.router-link-exact-active {
        color: #63e2b7;
      }
    }
  }
}

#content-area {
  margin: 4rem auto;
  max-width: 800px;
}
</style>
