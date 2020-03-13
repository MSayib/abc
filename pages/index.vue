<template>
 <div>
  <carousel />
    <v-row>
      <v-col
        cols="12"
        md="8"
      >
        <v-card
          class="pa-2"
          outlined
          tile
        >
          
         <post />
        </v-card>
      </v-col>
      <v-col
        cols="6"
        md="4"
      >
        <v-card
          class="pa-2"
          outlined
          tile
        >
         <sidebar />
        </v-card>
      </v-col>
    </v-row>

  <page />
 </div>
</template>


<script>
import Carousel from '~/components/Carousel'
import Post from '~/components/post'
import Sidebar from '~/components/Sidebar'
import Page from '~/components/pagination'
import Postcrud from '~/components/postcrud'

export default {
  components: {
    Carousel,
    Post,
    Sidebar,
    Page,
    Postcrud
  },
}
</script>
