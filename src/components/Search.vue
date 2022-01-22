<template>
  <n-space vertical class="search-space">
    <n-input
      v-model:value="query"
      clearable
      type="text"
      size="large"
      placeholder="Search"
      @keyup.enter="search"
    />
    <n-space>
      <n-button type="primary" @click="search" size="large">Search</n-button>
      <n-switch v-model:value="useSiteFilter">
        <template #checked>Filter sites</template>
        <template #unchecked>Unfiltered</template>
      </n-switch>

      <n-switch v-model:value="useDuck">
        <template #checked>duck.com</template>
        <template #unchecked>google.com</template>
      </n-switch>
    </n-space>

    <n-dynamic-input v-model:value="sites" placeholder="example.com" />

    <code>{{ fullQuery }}</code>
  </n-space>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import { NButton, NDynamicInput, NInput, NSpace, NSwitch } from "naive-ui";

export default defineComponent({
  components: {
    NButton,
    NDynamicInput,
    NInput,
    NSpace,
    NSwitch,
  },

  data: function () {
    return {
      useSiteFilter: true,
      useDuck: true,
      query: "",
      sites: ["stackoverflow.com", "github.com"],
    };
  },

  computed: {
    fullQuery(): string {
      if (this.query.length === 0) return "";
      const siteFilters = this.useSiteFilter
        ? `(${this.sites.map((site) => `site:${site}`).join(" | ")})`
        : "";
      return `${this.query} ${siteFilters}`;
    },

    searchUrl(): string {
      return this.useDuck ? "duck.com/" : "google.com/search";
    },
  },

  methods: {
    search() {
      window.open(`https://${this.searchUrl}?q=${this.fullQuery}`);
    },
  },

  watch: {
    sites(newSites) {
      localStorage.setItem("sites", newSites);
    },
  },

  beforeMount() {
    this.sites = (localStorage.getItem("sites") || "stackoverflow.com").split(",");
  },
});
</script>

<style scoped lang="scss">
.search-space {
  margin: 4rem auto;
  max-width: 600px;
}
</style>
