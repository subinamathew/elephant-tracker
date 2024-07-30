<template>
  <v-expansion-panel>
    <v-expansion-panel-header>
      {{ node.title }}
    </v-expansion-panel-header>
    <v-expansion-panel-content>
      <v-list dense>
        <v-list-item v-for="device in node.devices" :key="device.id">
          <device :device="device" />
        </v-list-item>
      </v-list>
    </v-expansion-panel-content>
  </v-expansion-panel>
</template>

<script>
export default {
  name: 'Node',
  props: {
    node: {
      type: Object,
      required: true,
    },
  },
};
</script>
