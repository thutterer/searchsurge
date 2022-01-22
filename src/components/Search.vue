<template>
  <n-space vertical>
    <n-space justify="space-between" class="search-bar">
      <n-select
        v-model:value="searchUrl"
        :options="searchEngines"
        :default-value="searchEngines[0].label"
        size="large"
      />
      <n-input
        v-model:value="query"
        autofocus
        clearable
        type="text"
        size="large"
        placeholder="Search"
        @keyup.enter="search"
      />
      <n-button type="primary" @click="search" size="large">Search</n-button>
    </n-space>

    <n-slider
      v-model:value="filter"
      :marks="marks"
      step="mark"
      :tooltip="false"
    />

    <n-card v-if="filter === 50" title="Blocked sites">
      <n-dynamic-input v-model:value="blockedSites" placeholder="example.com" />
    </n-card>

    <n-card v-if="filter === 100" title="Allowed sites">
      <n-dynamic-input v-model:value="allowedSites" placeholder="example.com" />
    </n-card>

    <code>{{ fullQuery }}</code>
  </n-space>
</template>

<script lang="ts">
import { defineComponent } from "vue";
import {
  NButton,
  NCard,
  NDynamicInput,
  NInput,
  NSelect,
  NSlider,
  NSpace,
} from "naive-ui";

export default defineComponent({
  components: {
    NButton,
    NCard,
    NDynamicInput,
    NInput,
    NSelect,
    NSlider,
    NSpace,
  },

  data: function () {
    return {
      useSiteFilter: true,
      filter: 0,
      marks: { 0: "All", 50: "Block", 100: "Allow" },
      query: "",
      allowedSites: [""],
      blockedSites: [""],
      searchEngines: [
        {
          label: "DuckDuckGo",
          value: "duck.com",
        },
        {
          label: "Google",
          value: "google.com/search",
        },
      ],
      searchUrl: "duck.com",
    };
  },

  computed: {
    fullQuery(): string {
      if (this.query.length === 0) return "";

      let siteFilters = "";
      switch (this.filter) {
        case 50:
          siteFilters = `${this.blockedSites
            .map((site) => `-site:${site}`)
            .join(" ")}`;
          break;
        case 100:
          siteFilters = `(${this.allowedSites
            .map((site) => `site:${site}`)
            .join(" | ")})`;
      }

      return `${this.query} ${siteFilters}`;
    },
  },

  methods: {
    search() {
      window.open(`https://${this.searchUrl}?q=${this.fullQuery}`);
    },
  },

  watch: {
    allowedSites(newAllowedSites) {
      localStorage.setItem("allowedSites", newAllowedSites);
    },
  },

  beforeMount() {
    this.allowedSites = (
      localStorage.getItem("allowedSites") || "stackoverflow.com"
    ).split(",");

    this.blockedSites = (localStorage.getItem("blockedSites") || "")
      .split(",")
      .filter((entry) => entry.trim() != "");
  },
});
</script>

<style lang="scss">
.search-bar {
  > * {
    flex-grow: 1;
  }
  > :nth-child(2) {
    flex-grow: 100;
  }
  > :nth-child(3) button {
    width: calc(100% - 6px);
  }
}

.n-slider .n-slider-marks .n-slider-mark {
  color: #e8e8e8;
}
</style>
