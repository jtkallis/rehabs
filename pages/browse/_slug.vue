<template>
  <div>
    <Breadcrumbs :location="location" :back-more="back_more" :back="back" />
    <Listing :listing="listing" :prevpage="prev" :nextpage="next" />
    <ListingCard :listings="listings" />
    <Footer :cities="cities" />
  </div>
</template>
<script>
import Listing from '@/components/ListingClass'

export default {
  async asyncData({ $axios, params }) {
    const baseURL = $axios.defaults.baseURL
    const url = baseURL + '/api/listing/' + params.slug
    return await $axios.$get(url).then((res) => {
      const Listings = []
      let i
      for (i = 0; i < res.listings.length; i++) {
        Listings.push(new Listing(res.listings[i]))
      }
      const listing = new Listing(res.listing)

      return {
        listing,
        listings: Listings,
        location: listing.location,
        cities: res.cities,
        next: res.next,
        prev: res.prev,
        back:
          '/states/' +
          res.listing.location.slug_state_name +
          '/city/' +
          res.listing.location.slug_city_name,
        back_more: '/states/' + res.listing.location.slug_state_name
      }
    })
  },
  data() {
    return {
      listingName: null,
      location: null,
      next: null,
      prev: null,
      back_more: null,
      back: null
    }
  },
  methods: {
    formatDate(date) {
      const options = { year: 'numeric', month: 'long', day: 'numeric' }
      return new Date(date).toLocaleDateString('en', options)
    }
  }
}
</script>
<style>
.nuxt-content p {
  margin-bottom: 20px;
}
.nuxt-content h2 {
  font-weight: bold;
  font-size: 28px;
}
.nuxt-content h3 {
  font-weight: bold;
  font-size: 22px;
}
.icon.icon-link {
  background-image: url('~assets/svg/icon-hashtag.svg');
  display: inline-block;
  width: 20px;
  height: 20px;
  background-size: 20px 20px;
}
</style>
