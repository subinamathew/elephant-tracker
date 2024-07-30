<template>
    <v-list-item-title>ss{{ device.name }}</v-list-item-title>
  </template>
  
  <script>
  export default {
    name: 'Device',
    props: {
      device: {
        type: Object,
        required: true,
      },
    },
  };
  </script>
  