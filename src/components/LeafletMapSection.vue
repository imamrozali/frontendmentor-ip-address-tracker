<template>
  <div class="min-h-screen z-0"></div>
</template>

<script>
import 'leaflet/dist/leaflet.css';
import 'leaflet/dist/leaflet.js';

export default {
  name: 'LeafletMapSection',
  props: ['location'],
  data() {
    return {};
  },
  mounted() {
    this.generateMap();
  },
  watch: {
    location() {
      this.generateMap();
    }
  },
  methods: {
    generateMap() {
      this.$nextTick(() => {
        if (window.L.DomUtil.get(this.$el)) {
          window.L.DomUtil.get(this.$el)._leaflet_id = null;
        }
        let map = new window.L.map(this.$el).setView(this.location, 13);

        window.L.tileLayer(
          'https://api.mapbox.com/styles/v1/{id}/tiles/{z}/{x}/{y}?access_token={accessToken}',
          {
            attribution:
              'Map data &copy; <a href="https://www.openstreetmap.org/">OpenStreetMap</a> contributors, <a href="https://creativecommons.org/licenses/by-sa/2.0/">CC-BY-SA</a>, Imagery © <a href="https://www.mapbox.com/">Mapbox</a>',
            maxZoom: 18,
            id: 'mapbox/streets-v11',
            tileSize: 512,
            zoomOffset: -1,
            accessToken: process.env.VUE_APP_MAPBOX_TOKEN
          }
        ).addTo(map);

        var icon = window.L.icon({
          iconUrl: require('../assets/images/icon-location.svg'),
          iconSize: [46, 58] // size of the icon
        });

        window.L.marker(this.location, { icon: icon }).addTo(map);
      });
    }
  }
};
</script>

<style lang="css" scoped></style>
