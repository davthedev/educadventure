<template>
  <q-page class="flex">
    <div style="flex:1">
      <l-map ref="map" :zoom="zoom" :center="center" :options="mapOptions" :crs="crs">
        <l-tile-layer :url="url" :attribution="attribution"/>

        <l-marker v-for="(pin, k) in pins" :key="k" :lat-lng="pin.latlng" :icon="icon">
          <l-popup >
            <p>{{pin.name}}</p>
            <q-btn color="primary" @click="accessPinData(pin.datakey)">Go there</q-btn>
          </l-popup>
        </l-marker>
      </l-map>
    </div>

  </q-page>
</template>

<script>
import { LMap, LTileLayer, LMarker, LPopup, LIcon } from 'vue2-leaflet'
import L from 'leaflet'
import { CRS, icon } from 'leaflet'
import 'leaflet/dist/leaflet.css'

export default {
  name: 'Map',
  components: {
    LMap,
    LTileLayer,
    LMarker,
    LPopup,
    LIcon,
  },
  data () {
    return {


      pins: [
        {name:"Challenge 1", datakey:0, latlng:[-50, 50]},
        {name:"Challenge 2", datakey:1, latlng:[-30, 50]},
      ],


      crs: CRS.Simple,
      map: null,
      mapOptions: {
        scrollWheelZoom: false,
        doubleClickZoom: false,
        maxBounds: [[0, 0], [-128, 256]],
        noWrap: true,
        zoomControl: false,
      },
      zoom: 4,
      minZoom: 4,
      maxZoom: 4,
      center: [-50, 100],
      url: 'statics/maps/fantasy/12/tile_{x}-{y}.png',

      icon: icon({
        iconUrl: "statics/maps/pins/Pin1.png",
        iconSize: [52, 84],
        iconAnchor: [26, 84],
        popupAnchor: [0, -84],
      }),
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.map = this.$refs.map.mapObject // work as expected
    })
  },
  methods: {
    accessPinData: function(datakey) {
      console.log("Open pin data " + datakey)

      this.$router.push('/mission')
    }
  }
}
</script>
<style>
</style>
