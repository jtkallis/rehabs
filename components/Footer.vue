<template>
  <div class="m-8">
    <h1 class="font-bold text-2xl">Local Listings</h1>
    <footer class="flex justify-center border-gray-500 border-t-2 font-medium">
      <ul
        v-if="states"
        class="grid lg:grid-cols-8 md:grid-cols-6 sm:grid-cols-4 xs:grid-cols-3 divide-x divide-blue-800"
      >
        <li v-for="(state, id) in states" :key="id" class="inline p-5">
          <a :href="`/states/${state.slug_state_name}`">{{
            state.state_name
          }}</a>
        </li>
      </ul>
      <ul
        v-if="cities"
        class="grid lg:grid-cols-8 md:grid-cols-6 sm:grid-cols-4 xs:grid-cols-3 divide-x divide-blue-800"
      >
        <li v-for="(city, id) in cities" :key="id" class="inline p-5">
          <a
            :href="`/states/${city.slug_state_name}/city/${city.slug_city_name}`"
            >{{ city.city_name }}</a
          >
        </li>
      </ul>
    </footer>
  </div>
</template>
<script>
export default {
  props: {
    states: {
      type: Array,
      default: () => null
    },
    cities: {
      type: Array,
      default: () => null
    }
  }
}
</script>
<style class="postcss">
.listing-card {
  border-radius: 8px;
}
.listing-card a {
  background-color: #fff;
  border-radius: 8px;
}
.listing-card img div {
  border-radius: 8px 0 0 8px;
}
</style>
