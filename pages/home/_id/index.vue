<template>
  <v-card style="width: 100%" class="mx-auto" max-width="344">
    <v-img
      src="https://cdn.vuetifyjs.com/images/cards/sunshine.jpg"
      height="200px"
    ></v-img>

    <v-card-title>{{ post.judul }}</v-card-title>
    <v-card-subtitle> By : {{ post.penulis }} </v-card-subtitle>

    <v-card-actions>
      <nuxt-link style="text-decoration: none;" to="/home">
        <v-btn text>Kembali</v-btn>
      </nuxt-link>
      <v-btn color="purple" text>
        Edit
      </v-btn>

      <v-spacer></v-spacer>

      <v-btn icon @click="show = !show">
        <v-icon>{{ show ? "mdi-chevron-up" : "mdi-chevron-down" }}</v-icon>
      </v-btn>
    </v-card-actions>

    <v-expand-transition>
      <div v-show="show">
        <v-divider></v-divider>

        <v-card-text>
          {{ post.isi }}
        </v-card-text>
      </div>
    </v-expand-transition>
  </v-card>
</template>

<script>
export default {
  data() {
    return {
      show: false,
      post: {},
      id: this.$route.params.id
    };
  },
  mounted() {
    this.$axios
      .get("http://localhost:3002/posts/" + this.$route.params.id)
      .then(res => {
        this.post = res.data || {};
      });
  }
};
</script>
