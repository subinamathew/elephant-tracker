<template>
  <v-app>
    <AppHeader />
    <AppNavigation />

    <v-main>
      <router-view />
      <AppBody></AppBody>
    </v-main>

    <AppFooter />
  </v-app>
</template>

<script setup>
  //
</script>
