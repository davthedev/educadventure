<template>
  <q-page class="flex">
    <div style="flex:1">
      <l-map ref="map" :zoom="zoom" :center="center" :options="mapOptions" :crs="crs">
        <l-tile-layer :url="url" :attribution="attribution"/>

      <l-marker :lat-lng="[-50, 50]" />
      </l-map>
    </div>

  </q-page>
</template>

<script>
import { LMap, LTileLayer, LMarker } from 'vue2-leaflet'
import L from 'leaflet'
import { CRS } from 'leaflet'
import 'leaflet/dist/leaflet.css'

export default {
  name: 'Map',
  components: {
    LMap,
    LTileLayer,
    LMarker,
  },
  data () {
    return {
      crs: CRS.Simple,
      map: null,
      mapOptions: {
        scrollWheelZoom: false,
        maxBounds: [[0, 0], [-128, 256]],
        noWrap: true,
        zoomControl: false,
      },
      zoom: 4,
      minZoom: 4,
      maxZoom: 4,
      center: [-50, 100],
      url: 'statics/maps/fantasy/12/tile_{x}-{y}.png',
    }
  },
  mounted() {
    this.$nextTick(() => {
      this.map = this.$refs.map.mapObject // work as expected
    })
  }
}
</script>
<style>
</style>
