<template>
  <v-navigation-drawer :value="internalDrawer" app>
    <v-list nav dense>
      <v-list-item link>
        <v-icon>mdi-home</v-icon>
        <v-list-item-title>Home</v-list-item-title>
      </v-list-item>
      <v-list-item link>
        <v-icon>mdi-icon</v-icon>
        <v-list-item-title>About</v-list-item-title>
      </v-list-item>
    </v-list>
  </v-navigation-drawer>
</template>

<script setup>
import { ref, watch } from 'vue';

const props = defineProps({
  drawer: {
    type: Boolean,
    required: true,
  },
});

const emit = defineEmits(['update:drawer']);

const internalDrawer = ref(props.drawer);

watch(internalDrawer, (newValue) => {
  emit('update:drawer', newValue);
});
</script>
