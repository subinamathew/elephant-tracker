<template>
  <v-app id="inspire">
    <Navigation v-model="drawer" />
    <v-app-bar>
      <v-app-bar-nav-icon @click="drawer = !drawer"></v-app-bar-nav-icon>

      <v-app-bar-title>🐘 Elephant Tracker: v0.0.1</v-app-bar-title>
    </v-app-bar>

    <v-main>
      <v-container>
        <v-row>
          <h3>Area A</h3>: &nbsp;
          <span v-if="alertNodesCountA > 0">
            {{ alertNodesCountA }} out of {{ totalNodesCountA }} nodes have alert status.
          </span>      
          <v-col cols="12">
            <v-data-iterator :items="filteredNodesA">
              <template v-slot:default="{ items, isExpanded, toggleExpand }">
                <v-row>
                  <v-col
                    v-for="item in items"
                    :key="item.raw.title"
                    cols="12"
                    md="4"
                    sm="12"
                  >
                    <v-card>
                      <v-card-title class="d-flex align-center" :style="{ backgroundColor: item.raw.status === 'Online' ? 'blue' : 'red' }">
                        <v-icon
                          :color="item.raw.status === 'Online' ? 'blue' : 'white' "
                          :icon="item.raw.icon"
                          size="18"
                          start
                        ></v-icon>

                        <h4>{{ item.raw.title }}</h4>
                      </v-card-title>

                      <v-card-text>
                        {{ item.raw.description }}
                      </v-card-text>

                      <div class="px-4">
                        <v-switch
                          :label="`${isExpanded(item) ? 'Hide' : 'Show'} details`"
                          :model-value="isExpanded(item)"
                          density="compact"
                          inset
                          @click="() => toggleExpand(item)"
                        ></v-switch>
                      </div>

                      <v-divider></v-divider>

                      <v-expand-transition>
                        <div v-if="isExpanded(item)">
                          <v-list :lines="false" density="compact">
                            <v-list-item :title="`🏷️ ID: ${item.raw.id}`" active></v-list-item>
                            <v-list-item :title="`📍 Location Code: ${item.raw.location ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🧭 Status: ${item.raw.status ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🐘 Last Trigger: ${item.raw.trigger ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🐝 Bee Trigger: ${item.raw.sound ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`📡 Signal: ${item.raw.connection ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🔋 Battery: ${item.raw.charge ||  'unavailable'}`"></v-list-item>

                          </v-list>
                        </div>
                      </v-expand-transition>
                    </v-card>
                  </v-col>
                </v-row>
              </template>
            </v-data-iterator>

          </v-col>
        </v-row>
        <v-row>
          <h3>Area B</h3>: &nbsp;
          <span v-if="alertNodesCountB > 0">
            {{ alertNodesCountB }} out of {{ totalNodesCountB }} nodes have alert status.
          </span>            
          <v-col cols="12">
            <v-data-iterator :items="filteredNodesB">
              <template v-slot:default="{ items, isExpanded, toggleExpand }">
                <v-row>
                  <v-col
                    v-for="item in items"
                    :key="item.raw.title"
                    cols="12"
                    md="4"
                    sm="12"
                  >
                    <v-card>
                      <v-card-title class="d-flex align-center" :style="{ backgroundColor: item.raw.status === 'Online' ? 'blue' : 'red' }">
                        <v-icon
                          :color="item.raw.status === 'Online' ? 'blue' : 'white' "
                          :icon="item.raw.icon"
                          size="18"
                          start
                        ></v-icon>

                        <h4>{{ item.raw.title }}</h4>
                      </v-card-title>

                      <v-card-text>
                        {{ item.raw.description }}
                      </v-card-text>

                      <div class="px-4">
                        <v-switch
                          :label="`${isExpanded(item) ? 'Hide' : 'Show'} details`"
                          :model-value="isExpanded(item)"
                          density="compact"
                          inset
                          @click="() => toggleExpand(item)"
                        ></v-switch>
                      </div>

                      <v-divider></v-divider>

                      <v-expand-transition>
                        <div v-if="isExpanded(item)">
                          <v-list :lines="false" density="compact">
                            <v-list-item :title="`🏷️ ID: ${item.raw.id}`" active></v-list-item>
                            <v-list-item :title="`📍 Location Code: ${item.raw.location ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🧭 Status: ${item.raw.status ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🐘 Last Trigger: ${item.raw.trigger ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🐝 Bee Trigger: ${item.raw.sound ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`📡 Signal: ${item.raw.connection ||  'unavailable'}`"></v-list-item>
                            <v-list-item :title="`🔋 Battery: ${item.raw.charge ||  'unavailable'}`"></v-list-item>

                          </v-list>
                        </div>
                      </v-expand-transition>
                    </v-card>
                  </v-col>
                </v-row>
              </template>
            </v-data-iterator>

          </v-col>
        </v-row>
      </v-container>
    </v-main>

  </v-app>
</template>

<script setup>
import { ref } from 'vue';
import Navigation from './components/Navigation.vue';
import Node from './components/Node.vue';

const nodes = ref([
{
    id: 55510,
    title: 'Karadikkal',

      color: 'primary',
      icon: 'mdi-map-marker',
      description: 'Karadikkal checkpost',
      location: 'A123',
      status: 'Online',
      trigger: '2023-08-05 10:00:00',
      sound: 'false',
      connection: '85%',
      charge: '75%',
      node_group: 'a'

  },
  {
    id: 55510,
    title: 'Edayahalli',

      color: 'primary',
      icon: 'mdi-map-marker',
      description: 'Edayahalli Bypass',
      location: 'A123',
      status: 'Online',
      trigger: '2023-08-05 10:00:00',
      sound: 'false',
      connection: '85%',
      charge: '75%',
      node_group: 'b'

  },
  {
    id: 85510,
    title: 'Madeshwara',
      color: 'primary',
      icon: 'mdi-map-marker',
      description: 'Madeshwara Node 2.',
      location: 'A1223',
      status: 'Alert',
      trigger: '2023-08-05 10:00:00',
      sound: 'false',
      connection: '95%',
      charge: '75%',
      node_group: 'a'

  },
  {
    id: 25510,
    title: 'Guttiyalattur',

      color: 'primary',
      icon: 'mdi-map-marker',
      description: 'Highway Guttiyalattur.',
      location: 'A123',
      status: 'Online',
      trigger: '2023-08-05 10:00:00',
      sound: 'false',
      connection: '85%',
      charge: '75%',
      node_group: 'b'

  },
  {
    id: 35510,
    title: 'Doddasampige',

      color: 'primary',
      icon: 'mdi-map-marker',
      description: 'Doddasampige Area',
      location: 'A123',
      status: 'Alert',
      trigger: '2023-08-05 10:00:00',
      sound: 'false',
      connection: '85%',
      charge: '75%',
      node_group: 'b'

  },
]);
const filteredNodesA = computed(() => nodes.value.filter(node => node.node_group === 'a'));
const filteredNodesB = computed(() => nodes.value.filter(node => node.node_group === 'b'));
const alertNodesCountA = computed(() => filteredNodesA.value.filter(node => node.status === 'Alert').length);
const totalNodesCountA = computed(() => filteredNodesA.value.length);

const alertNodesCountB = computed(() => filteredNodesB.value.filter(node => node.status === 'Alert').length);
const totalNodesCountB = computed(() => filteredNodesB.value.length);
const expandedA = ref(true);
const expandedB = ref(true);

const drawer = ref(false);
</script>