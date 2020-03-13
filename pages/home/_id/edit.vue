<template>
  <div>
    <v-row>
      <v-col cols="12" sm="4"> </v-col>
      <v-col cols="12" sm="4">
        <v-text-field v-model="post.id" label="Id" outlined></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" sm="4"> </v-col>
      <v-col cols="12" sm="4">
        <v-text-field
          v-model="post.judul"
          label="Judul"
          outlined
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" sm="4"> </v-col>
      <v-col cols="12" sm="4">
        <v-text-field v-model="post.isi" label="isi" outlined></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="12" sm="4"> </v-col>
      <v-col cols="12" sm="4">
        <v-text-field
          v-model="post.penulis"
          label="Penulis"
          outlined
        ></v-text-field>
      </v-col>
    </v-row>
    <v-row>
      <v-col cols="7" sm="4"> </v-col>
      <v-col cols="5" sm="4">
        <v-btn @click.prevent="simpan" color="success" large dark>
          Simpan
        </v-btn>
      </v-col>
    </v-row>
  </div>
</template>

<script>
export default {
  data() {
    return {
      post: {}
    };
  },
  mounted() {
    this.getDetail();
  },
  methods: {
    getDetail() {
      this.$axios
        .get("http://localhost:3002/posts/" + this.$route.params.id)
        .then(res => {
          this.post = res.data || {};
        });
    },
    simpan() {
      this.$axios
        .patch(
          "http://localhost:3002/posts/" + this.$route.params.id,
          this.post
        )
        .then(send => {
          this.$router.push("/home");
        });
    }
  }
};
</script>
