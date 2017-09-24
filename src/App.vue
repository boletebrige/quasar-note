<template>
  <q-layout
    ref="layout"
    view="lHh Lpr fff"
    :left-class="{'bg-grey-2': true}"
  >
    <q-toolbar slot="header" color="dark">
      <!-- <q-btn
        flat
        @click="$refs.layout.toggleLeft()"
      >
        <q-icon name="menu" />
      </q-btn> -->

      <q-toolbar-title class="text-center">
        Quasar Notes
        <div slot="subtitle">Running on Quasar v{{$q.version}}</div>
      </q-toolbar-title>
      <!-- <q-btn
          flat
          @click="$refs.layout.toggleLeft()"
        >
        <q-icon name="menu" />
      </q-btn> -->
    </q-toolbar>

    <!-- <div slot="left">
      <q-list no-border link inset-delimiter>
        <q-side-link item to="/new">
          <q-item-side icon="new" />
          <q-item-main label="New" sublabel="quasar-framework.org" />
        </q-side-link>
      </q-list>
    </div> -->

    <!--
      Replace following <div> with
      <router-view /> component
      if using subRoutes
    -->
    <div id="q-app">
      <router-view />
    </div>
  </q-layout>
</template>

<script>
/*
 * Root component
 */
import {
  QLayout,
  QToolbar,
  QToolbarTitle,
  QBtn,
  QIcon,
  QList,
  QListHeader,
  QItem,
  QItemSide,
  QItemMain,
  QSideLink
} from 'quasar'

export default {
  components: {
    QLayout,
    QToolbar,
    QToolbarTitle,
    QBtn,
    QIcon,
    QList,
    QListHeader,
    QItem,
    QItemSide,
    QItemMain,
    QSideLink
  },
  data () {
    return {
    }
  },
  computed: {
  },
  methods: {
  },
  mounted () {
  },
  beforeDestroy () {
  }
}
</script>

<style></style>
