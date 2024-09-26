<script setup lang="ts">
const items = [
  [{
    label: 'Speed Test',
    icon: 'i-heroicons-rocket-launch-20-solid',
    to: 'speedTest',
  }, {
    label: 'Parts Finder',
    icon: 'i-heroicons-wrench-20-solid',
    disabled: true
  }]
]
</script>
<template>
  <header>
    <div class="mx-auto max-w-7xl flex items-center justify-between">
      <NuxtLink to="/">
        <NuxtImg src="/logo.svg" alt="logo" width="200px" />
      </NuxtLink>

      <UDropdown :items="items" :popper="{ placement: 'bottom-start' }">
        <UButton color="green" label="Сервисы" trailing-icon="i-heroicons-chevron-down-20-solid" />
      </UDropdown>
    </div>

  </header>
</template>
<style lang="scss">

</style>