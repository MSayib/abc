<template>
<div>   
  <v-carousel :show-arrows="false">
    <v-carousel-item
      v-for="(item,i) in items"
      :key="i"
      :src="item.src"
    ></v-carousel-item>
  </v-carousel>
</div>
</template>

<script>

  import Image1 from '~/assets/images/slider2.jpg'
  import Image2 from '~/assets/images/slider3.jpg'
  import Image3 from '~/assets/images/slider1.jpg'
  

  export default {
    data () {
      return {
        items: [
          {
            src: Image1,
          },
          {
            src: Image2,
          },
         {
            src: Image3,
          }
        ],
      }
    },
  }
</script>
