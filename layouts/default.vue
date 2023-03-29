<template>
  <main>
    <ThemeSwitcher />
    <nuxt />
  </main>
</template>

<script lang="ts">
import ThemeSwitcher from '~/components/ThemeSwitcher.vue';
export default {
  components: {
    ThemeSwitcher,
  },
};
</script>