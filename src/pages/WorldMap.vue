<template>
  <q-page class="flex">
    <div style="flex:1">
      <l-map ref="map" :zoom="zoom" :center="center" :options="mapOptions" :crs="crs">
        <l-tile-layer :url="url"/>

        <template v-for="(pin, k) in pins">
          <l-marker v-if="unlocked_missions[pin.datakey]" :key="k" :lat-lng="pin.latlng" :icon="completed_missions[pin.datakey] ? icon_complete : icon">
            <l-popup >
              <p>{{pin.name}}</p>
              <!-- <p v-if="unlocked_missions[pin.datakey]">Unlocked</p><p v-else>Locked</p>
              <p v-if="completed_missions[pin.datakey]">Complete</p><p v-else>Unfinished</p> -->
              <q-btn style="width: 160px" v-if="!completed_missions[pin.datakey]" color="white" text-color="accent" rounded unelevated @click="accessPinData(pin.datakey)" icon="double_arrow">START</q-btn>
              <q-btn style="width: 160px" v-else color="white" rounded outline disable icon="o_assignment_turned_in">COMPLETE</q-btn>
            </l-popup>
          </l-marker>
        </template>
      </l-map>
    </div>

    <q-page-sticky position="bottom" :offset="[0, 0]" style="z-index: 2000">
      <q-card class="miniboard">
        <q-card-section>
          <q-circular-progress
            :value="10"
            size="90px"
            :thickness="0.2"
            color="red-13"
            track-color="grey-8"
            class="q-ma-sm"
            show-value
          >
            <div class="caption"><span class="smalltitle">SPREAD</span>10</div>
          </q-circular-progress>
          <q-circular-progress
            :value="50"
            size="90px"
            :thickness="0.2"
            color="cyan-5"
            track-color="grey-8"
            class="q-ma-sm"
            show-value
          >
            <div class="caption"><span class="smalltitle">LEVEL</span>3</div>
          </q-circular-progress>
          <q-circular-progress
            :value="30"
            size="90px"
            :thickness="0.2"
            color="yellow-12"
            track-color="grey-8"
            class="q-ma-sm"
            show-value
          >
            <div class="caption"><span class="smalltitle">GOODWILL</span>30</div>
          </q-circular-progress>

        </q-card-section>
      </q-card>

    </q-page-sticky>

    <q-page-sticky position="top" :offset="[0, 0]" style="z-index: 2000">
      <q-card class="miniboardup">
        <q-card-section>
          
          <q-btn-dropdown color="white" icon="menu" rounded flat>
            <q-list dark class="gamemenu">
              <q-item clickable v-close-popup @click="resetGame">
                <q-item-section>
                  <q-item-label>Reset game</q-item-label>
                </q-item-section>
              </q-item>
            </q-list>
          </q-btn-dropdown>
        </q-card-section>
      </q-card>

    </q-page-sticky>


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

      dbgUnlockAll: false,

      pins: [
        {name:"Welcome! Here is the tutorial",    datakey:0, latlng:[-60, 125]},
        {name:"Soap making",                      datakey:1, latlng:[-40, 138]},
        {name:"Growing bacteria",                 datakey:2, latlng:[-52, 100]},
        {name:"Hy-giene",                         datakey:3, latlng:[-31, 115]},
        {name:"Super power",                      datakey:4, latlng:[-70, 138]},
        {name:"Fridge exploration",               datakey:5, latlng:[-40, 153]},
        {name:"Mens Sana",                        datakey:6, latlng:[-73, 148]},
        {name:"Soap coalition",                   datakey:7, latlng:[-79, 128]},
        {name:"Shapin' Cleanliness",              datakey:8, latlng:[-79, 136]},
        {name:"Bread experiment",                 datakey:9, latlng:[-50, 133]},
        {name:"Keep the bond",                    datakey:10, latlng:[-72, 100]},
        {name:"Law of soap",                      datakey:11, latlng:[-89, 143]},
        {name:"Is it war?",                       datakey:12, latlng:[-90, 110]},
      ],

      unlock_conditions: {
        0: [],
        1: [0],
        2: [0],
        3: [0],
        4: [0],
        5: [0],
        6: [0],
        7: [0],
        8: [1],
        9: [1, 2],
        10: [5, 6],
        11: [7],
        12: [10, 11],
      },

      unlocked_missions:{},
      completed_missions:{},


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
      
      icon_complete: icon({
        iconUrl: "statics/maps/pins/Pin3.png",
        iconSize: [52, 84],
        iconAnchor: [26, 84],
        popupAnchor: [0, -84],
      }),
    }
  },
  mounted() {
    this.updateUnlockStatus()
    this.$nextTick(() => {
      this.map = this.$refs.map.mapObject // work as expected
    })
  },
  methods: {
    accessPinData: function(datakey) {
      console.log("Open pin data " + datakey)

      this.$router.push('/mission/' + datakey)
    },

    resetGame: function() {
      let unlocked_missions = this.$gameglobals.unlocked_missions
      let completed_missions = this.$gameglobals.completed_missions

      for (var key in unlocked_missions) {
        unlocked_missions[key] = false
      }
      for (var key in completed_missions) {
        completed_missions[key] = false
      }

      this.unlocked_missions = unlocked_missions
      this.completed_missions = completed_missions
      this.$gameglobals.unlocked_missions = unlocked_missions
      this.$gameglobals.completed_missions = completed_missions

      this.updateUnlockStatus()
    },

    // Update all unlock status of missions
    updateUnlockStatus: function() {

      let unlocked_missions = this.$gameglobals.unlocked_missions
      let completed_missions = this.$gameglobals.completed_missions

      for (var key in this.unlock_conditions) {
        console.log("Key " + key)
        let cond = this.unlock_conditions[key]
        let result = true
        cond.map((which_completed) => {
          // Check if this mission is complete
          if (!completed_missions[which_completed]) {
            result = false
          }
        })
        if (result == true || this.dbgUnlockAll) {
          console.log("unlocking mission " + key)
          unlocked_missions[key] = true
        }
      }

      this.unlocked_missions = unlocked_missions
      this.completed_missions = completed_missions
      this.$gameglobals.unlocked_missions = unlocked_missions
      this.$gameglobals.completed_missions = completed_missions
    }
  }
}
</script>
<style lang="sass">
.leaflet-container
  background-color: $blue-grey-9
  background-image: repeating-linear-gradient(45deg, transparent, transparent 35px, rgba(255,255,255,.05) 35px, rgba(255,255,255,.05) 70px)

.leaflet-popup-content
  font-family: "Roboto", "-apple-system", "Helvetica Neue", Helvetica, Arial, sans-serif
  font-size: 16px

.leaflet-popup-content .q-btn__content
  font-family: "Roboto", "-apple-system", "Helvetica Neue", Helvetica, Arial, sans-serif
  line-height: 1.5
  font-size: 14px

.leaflet-popup-content-wrapper
  background-color: $accent
  color: white
  border-radius: 24px


.leaflet-popup-content-wrapper .leaflet-popup-content 
  margin: 26px 26px
  text-align: center

.leaflet-popup-tip-container

.leaflet-popup-tip
  background-color: $accent

.leaflet-container a.leaflet-popup-close-button
  font-size: 20px
  color: white
  padding: 10px 30px

.miniboard
  border-radius: 60px 60px 0 0
  background-color: $grey-9
  color: white

  .caption
    font-size: 34px
    text-align: center

  .smalltitle
    font-size: 10px
    display: block
    font-weight: 500

.miniboardup
  border-radius: 0 0 30px 30px
  background-color: $grey-9
  color: white
  .q-card__section--vert
    padding-top: 5px
    padding-bottom: 5px

.gamemenu
  background-color: $accent
  width: 200px
  font-weight: 400
  font-size: 16px

</style>
