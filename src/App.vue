<template>
  <div id="app" class="overflow-hidden">
    <header class="h-56 flex flex-col items-center">
      <h1 class="pt-6 text-2xl font-medium text-white tracking-wider">
        IP Address Tracker
      </h1>

      <div class="flex justify-center pt-4 md:w-full">
        <input
          type="text"
          class="px-4 py-2 md:w-1/3 border rounded-tl-md rounded-bl-md text-sm text-gray-800 tracking-wider leading-none focus:outline-none focus:shadow-outline focus:bg-gray-100"
          placeholder="Search for any IP address or domain"
          v-model="search"
        />
        <button
          class="inline-block w-10 flex items-center justify-center bg-gray-900 hover:opacity-75 focus:outline-none focus:shadow-outline border-0 rounded-tr-md rounded-br-md"
          @click="getLocation"
        >
          <svg xmlns="http://www.w3.org/2000/svg" width="11" height="14">
            <path fill="none" stroke="#FFF" stroke-width="3" d="M2 1l6 6-6 6" />
          </svg>
        </button>
      </div>
    </header>

    <section
      class="absolute inset-x-0 -mt-20 w-3/4 md:flex py-2 md:p-6 mx-auto bg-white rounded-lg z-10 shadow-lg"
    >
      <Card class="md:w-1/4 border-r-2" title="IP Address" :body="ipAddress" />

      <Card
        class="md:w-1/4 border-r-2 rounded"
        title="Location"
        :body="location"
      />

      <Card
        class="md:w-1/4 border-r-2 rounded"
        title="Timezone"
        :body="timezone"
      />

      <Card class="md:w-1/4" title="ISP" :body="data.isp" />
    </section>

    <LeafletMapSection :location="lat_long" />
  </div>
</template>

<script>
import Card from '@/components/Card.vue';
import LeafletMapSection from '@/components/LeafletMapSection.vue';

export default {
  name: 'App',
  components: {
    Card,
    LeafletMapSection
  },
  data() {
    return {
      search: '192.212.174.101',
      data: {}
    };
  },
  computed: {
    ipAddress() {
      return this.data.ip;
    },
    location() {
      let location = this.data.location;
      return `${location.region}, ${location.country} ${location.postalCode}`;
    },
    timezone() {
      return `UTC ${this.data.location.timezone}`;
    },
    lat_long() {
      let location = this.data.location;
      return [location.lat, location.lng];
    }
  },
  created() {
    this.$nextTick(() => {
      this.getLocation();
    });
  },
  methods: {
    getLocation() {
      let url = `https://geo.ipify.org/api/v1?apiKey=${process.env.VUE_APP_IPIFY_KEY}&ipAddress=${this.search}&domain=${this.search}`;
      fetch(url)
        .then(response => response.json())
        .then(data => (this.data = data));
    }
  }
};
</script>

<style>
@import url('https://fonts.googleapis.com/css2?family=Rubik:wght@400;500;700&display=swap');

#app {
  font-family: 'Rubik', sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
}

header {
  background: url('./assets/images/pattern-bg.png');
}
</style>
