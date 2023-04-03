<template>
  <div class="flex w-full bg-blue-200">
    <div class="w-full bg-white rounded shadow-lg p-8 m-4 w-full md:mx-auto">
      <Notification v-if="error" :message="error" />
      <h1 class="block w-full text-center text-grey-900 mb-6 text-5xl">
        Write a Review
      </h1>
      <form class="mb-4 md:flex md:flex-wrap" action="/" method="post">
        <div class="flex flex-col mb-4 md:w-full">
          <label
            class="mb-2 uppercase font-bold text-lg text-grey-900"
            for="accommodations_amenities"
            >Accommodations &amp; Amenities</label
          >
          <Dropdown
            id="accommodations_amenities"
            v-model="ratings.accommodations_amenities"
            name="accommodations_amenities"
            rating-type="accommodations_amenities"
          />
        </div>
        <div class="flex flex-col mb-4 md:w-full">
          <label
            class="mb-2 uppercase font-bold text-lg text-grey-900"
            for="treatmentEffectiveness"
            >Treatment Quality &amp; Effectiveness</label
          >
          <Dropdown
            id="treatmentEffectiveness"
            v-model="ratings.treatment_effectiveness"
            name="treatmentEffectiveness"
            rating-type="treatment_effectiveness"
          />
        </div>
        <div class="flex flex-col mb-4 md:w-full">
          <label
            class="mb-2 uppercase font-bold text-lg text-grey-900"
            for="mealsNutrition"
            >Meals &amp; Nutrition</label
          >
          <Dropdown
            id="mealsNutrition"
            v-model="ratings.meals_nutrition"
            name="mealsNutrition"
            rating-type="meals_nutrition"
          />
        </div>
        <div class="flex flex-col mb-6 md:w-full">
          <label
            class="mb-2 uppercase font-bold text-lg text-grey-900"
            for="title"
            >Review Title</label
          >
          <input
            id="title"
            v-model="title"
            class="border py-2 px-3 text-grey-900"
            type="text"
            name="title"
          />
        </div>
        <div class="flex flex-col mb-4 md:w-full">
          <label
            class="mb-2 uppercase font-bold text-lg text-grey-900"
            for="review"
            >Review</label
          >
          <textarea
            id="review"
            class="border py-2 px-3 text-grey-900 w-11/12 h-64"
            type="text"
            name="review"
          />
        </div>

        <div class="flex flex-col mb-4 md:w-1/2">
          <label
            class="mb-2 uppercase tracking-wide font-bold text-lg text-grey-900"
            for="display_name"
            >Your Name</label
          >
          <input
            id="display_name"
            class="border py-2 px-3 text-grey-900 md:mr-2"
            type="text"
            name="display_name"
          />
        </div>
        <div class="flex flex-col mb-4 md:w-1/2">
          <label
            class="mb-2 uppercase font-bold text-lg text-grey-900 md:ml-2"
            for="email"
            >Email Address</label
          >
          <input
            id="email"
            class="border py-2 px-3 text-grey-900 md:ml-2"
            type="email"
            name="email"
          />
        </div>
        <button
          class="block bg-teal-600 hover:bg-teal-500 text-white uppercase text-lg mx-auto p-4 rounded"
          type="submit"
        >
          Post Review
        </button>
      </form>
      <a
        class="block w-full text-center no-underline text-sm text-grey-500 hover:text-grey-700"
        href="/login"
        >Already have an account?</a
      >
    </div>
  </div>
</template>

<script>
import Dropdown from '@/components/form/Dropdown'
export default {
  components: { Dropdown },
  middleware: 'guest',

  data() {
    return {
      review: '',
      display_name: '',
      email: '',
      password: '',
      title: '',
      ratings: {
        accommodations_amenities: null,
        treatment_effectiveness: null,
        meals_nutrition: null
      },
      error: null
    }
  },
  methods: {
    async register() {
      try {
        await this.$axios.post('register', {
          username: this.display_name,
          email: this.email,
          password: this.password
        })

        await this.$auth.loginWith('local', {
          data: {
            email: this.email,
            password: this.password
          }
        })

        this.$router.push('/')
      } catch (e) {
        this.error = e.response.data.message
      }
    },
    addRating(key, val) {
      this.ratings[key] = val
    }
  }
}
</script>
