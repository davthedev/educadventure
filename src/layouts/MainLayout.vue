<template>
  <q-layout view="hHh lpR fFf">
    <!-- <q-header elevated>
      <q-toolbar>
        <q-btn
          flat
          dense
          round
          icon="menu"
          aria-label="Menu"
          @click="leftDrawerOpen = !leftDrawerOpen"
        />

        <q-toolbar-title>
          EducAdventure
        </q-toolbar-title>

        <div>Quasar v{{ $q.version }}</div>
      </q-toolbar>
    </q-header> -->

    <q-drawer
      v-model="leftDrawerOpen"
      overlay bordered
    >
      <q-list>



        <q-item
          clickable
          :to="item.route" exact
          v-for="(item, k) in menuItems" :key="k"
        >
          <q-item-section
            v-if="item.icon"
            avatar
          >
            <q-icon :name="item.icon" />
          </q-item-section>

          <q-item-section>
            <q-item-label>{{item.title}}</q-item-label>
          </q-item-section>
        </q-item>
      </q-list>
    </q-drawer>

    <q-page-container>
      <router-view />
    </q-page-container>
  </q-layout>
</template>

<script>
import EssentialLink from 'components/EssentialLink'

export default {
  name: 'MainLayout',

  components: {
    EssentialLink
  },

  data () {
    return {


      leftDrawerOpen: false,
      
      menuItems: [
        {
          title: 'Map page',
          icon: 'map',
          route: '/',
        },
        {
          title: 'Mission page',
          icon: 'school',
          route: '/mission',
        },
      ]
    }
  }
}
</script>
