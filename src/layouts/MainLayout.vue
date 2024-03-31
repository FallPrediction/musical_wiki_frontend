<template>
  <q-layout view="lHr lpR fff" id="layout">
    <q-header class="text-white" height-hint="98" id="header">
      <q-toolbar>
        <!-- <q-btn dense flat round icon="menu" @click="toggleLeftDrawer" /> -->

        <q-toolbar-title>
          <q-avatar>
            <img src="~assets/logo-no-background.svg" />
          </q-avatar>
          Musical Wiki
        </q-toolbar-title>
      </q-toolbar>

      <q-tabs align="left">
        <q-route-tab to="/actors" label="演員" />
      </q-tabs>
    </q-header>

    <!-- <q-drawer v-model="leftDrawerOpen" side="left" behavior="mobile"> -->
    <!-- drawer content -->
    <!-- </q-drawer> -->

    <q-page-container>
      <router-view />
    </q-page-container>

    <q-footer class="text-white" id="footer">
      <q-toolbar>
        <q-toolbar-title>
          <q-avatar>
            <img src="~assets/logo-no-background.svg" />
          </q-avatar>
        </q-toolbar-title>
      </q-toolbar>
    </q-footer>
  </q-layout>
</template>

<script>
import { ref } from "vue";

export default {
  setup() {
    const leftDrawerOpen = ref(false);

    return {
      leftDrawerOpen,
      toggleLeftDrawer() {
        leftDrawerOpen.value = !leftDrawerOpen.value;
      },
    };
  },
};
</script>
