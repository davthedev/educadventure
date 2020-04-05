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
        {name:"The toilet is dirty", datakey:0, latlng:[-47, 95]},
        {name:"How to wash your dishes", datakey:1, latlng:[-32, 130]},
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
<style lang="sass">
.leaflet-container
  background-color: $blue-grey-9
  background-image: repeating-linear-gradient(45deg, transparent, transparent 35px, rgba(255,255,255,.1) 35px, rgba(255,255,255,.1) 70px);

.leaflet-popup-content
  font-family: "Roboto", "-apple-system", "Helvetica Neue", Helvetica, Arial, sans-serif
  font-size: 14px

.leaflet-popup-content .q-btn__content
  font-family: "Roboto", "-apple-system", "Helvetica Neue", Helvetica, Arial, sans-serif
  line-height: 1.5
  font-size: 14px
</style>
