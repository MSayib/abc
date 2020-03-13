<template>
  <v-card
    class="mx-auto"
    height="600"
    width="600"
  >
    <v-navigation-drawer
      class="deep-white accent-4"
      light
      permanent
    >
      <v-list>
        <v-list-item
          v-for="item in items"
          :key="item.title"
          link
        >
          <v-list-item-icon>
            <v-icon>{{ item.icon }}</v-icon>
          </v-list-item-icon>

          <v-list-item-content>
            <v-list-item-title>{{ item.title }}</v-list-item-title>
          </v-list-item-content>
        </v-list-item>
      </v-list>

      <template v-slot:append>
        <div class="pa-2">
          <v-btn block>Category</v-btn>
        </div>
      </template>
    </v-navigation-drawer>
  </v-card>
</template>

<script>
  export default {
    data () {
      return {
        items: [
        { title: 'Sejarah', },
        { title: 'Percintaan', },
        { title: 'Biologi',},
        { title: 'Fisika',},
        { title: 'Kimia',},
        { title: 'DLL',},
        ],
      }
    },
  }
</script>