<template>
  <div>
    <div class="m-10 mt-5">
      <NuxtLink class="underline" to="/">Home</NuxtLink> ...
      <a :href="`${backMore}`" class="underline">{{ location.stateName }}</a>
      ... <a :href="`${back}`" class="underline">{{ location.cityName }}</a>
    </div>
  </div>
</template>

<script>
export default {
  props: {
    back: {
      type: Object,
      default: () => null
    },
    backMore: {
      type: Object,
      default: () => null
    },
    location: {
      type: Object,
      default: () => null
    }
  }
}
</script>
