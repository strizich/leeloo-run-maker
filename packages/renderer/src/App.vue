<template>
  <sd-layout>
    <template #content>
      <router-view />
    </template>
  </sd-layout>
</template>

<script lang="ts">
import {defineComponent} from 'vue';
export default defineComponent({
  name: 'App',
});
</script>

<style lang="scss">
  @use '../assets/fonts/Roboto';
  @import '../../../node_modules/@strizich/sdui/dist/scss/engine.scss';
  @import url('../../../node_modules/@strizich/sdui/dist/style.css');
</style>
