<template>
  <div />
</template>

<script lang="ts">
import Vue from 'vue';
enum ThemeMode {
  'light' = 'light',
  'dark' = 'dark',
  'auto' = 'auto',
}
export default Vue.extend({
  components: {},
  data() {
    return {
      theme: ThemeMode.auto,
    };
  },
  computed: {
    isDarkTheme(): boolean {
      return this.theme === ThemeMode.dark;
    },
    isLightTheme(): boolean {
      return this.theme === ThemeMode.light;
    },
    isAutoTheme(): boolean {
      return this.theme === ThemeMode.auto;
    },
  },
  mounted() {
    const darkModeMedia = '(prefers-color-scheme: dark)';
    const lightModeMedia = '(prefers-color-scheme: light)';
    const isDarkMode =
      window.matchMedia && window.matchMedia(darkModeMedia).matches;
    const isLightMode =
      window.matchMedia && window.matchMedia(lightModeMedia).matches;
    if (isDarkMode) {
      this.setTheme(ThemeMode.dark);
    }
    if (isLightMode) {
      this.setTheme(ThemeMode.light);
    }
    window.matchMedia(darkModeMedia).addListener((e) => {
      if (e.matches) {
        this.setTheme(ThemeMode.dark);
      }
    });
    window.matchMedia(lightModeMedia).addListener((e) => {
      if (e.matches) {
        this.setTheme(ThemeMode.light);
      }
    });
  },
  methods: {
    setTheme(theme: ThemeMode): void {
      this.theme = theme;
      Object.keys(ThemeMode).forEach((item) =>
        document.body.classList.remove(item)
      );
      document.body.classList.add(this.theme);
    },
  },
});
</script>