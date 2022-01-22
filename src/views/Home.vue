<template>
  <div class="home">
    <n-space justify="center">
      <img alt="Vue logo" src="../assets/logo.png" />
    </n-space>
    <Search />
  </div>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { NSpace } from "naive-ui";
import Search from "@/components/Search.vue"; // @ is an alias to /src

export default defineComponent({
  name: "Home",
  components: {
    NSpace,
    Search,
  },
});
</script>
