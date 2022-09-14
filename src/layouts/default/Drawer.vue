<template>
  <v-navigation-drawer
    id="default-drawer"
    v-model="drawer"
    :right="$vuetify.rtl"
    :mini-variant.sync="mini"
    mini-variant-width="80"
    app
    width="260"
  >
  <v-list-item class="mb-0 justify-space-between pl-3">
    <v-list-item-avatar>
      <v-img
        :src="
          require('@/assets/MARKy.png')"
      />
    </v-list-item-avatar>

    <v-list-item-content class="pl-2">
      <v-list-item-title class="text-h3">
        <strong class="mr-1 font-weight-black">MARKY</strong>
        <span class="primary--text">APP</span>
      </v-list-item-title>
    </v-list-item-content>
  </v-list-item>
    <div class="px-2">
      <default-drawer-header />
      <v-divider class="mx-3 mb-2" />
      <default-list :items="items" />
    </div>
    <template #append>
      <div class="pa-4 text-center">
        <vs-button
        href="/"
        danger
        >
        <v-icon
          color="white"
          >mdi-logout-variant</v-icon>
        <template #animate>
         Salir
        </template>
      </vs-button>
      </div>
    </template>
    <div class="pt-12" />
  </v-navigation-drawer>
</template>
<script>
  import Vue from 'vue'
  import Vuesax from 'vuesax'
  import 'vuesax/dist/vuesax.css'
  import { get, sync } from 'vuex-pathify'
  Vue.use(Vuesax, {
    // options here
  })
  export default {
    name: 'DefaultDrawer',
    components: {
      DefaultList: () => import(
        /* webpackChunkName: "default-list" */
        './List'
      ),
    },
    computed: {
      ...get('user', [
        'dark',
        'gradient',
        'image',
      ]),
      ...get('app', [
        'items',
        'version',
      ]),
      ...sync('app', [
        'drawer',
        'drawerImage',
        'mini',
      ]),
    },
  }
</script>

<style lang="sass">
#default-drawer
  .v-list-item
    margin-bottom: 8px

  .v-list-item::before,
  .v-list-item::after
    display: none

  .v-list-group__header__prepend-icon,
  .v-list-item__icon
    margin-top: 12px
    margin-bottom: 12px
    margin-left: 4px

  &.v-navigation-drawer--mini-variant
    .v-list-item
      justify-content: flex-start !important
</style>
