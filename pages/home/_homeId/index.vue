<template>
  <div>
    <nuxt-link :to="'/home'">back</nuxt-link>
    <nuxt-link :to="'/home/' + id + '/edit'">edit</nuxt-link>
    <h2>ini HALAMAN VIEW</h2>
    <h3>{{ orang.id }}</h3>id
    <p>{{ orang.name }}</p>nama
    <p>{{ orang.role }}</p>jabatan
  </div>
</template>

<script>
export default {
  data() {
    return {
      orang: {},
      id: this.$route.params.homeId
    };
  },
  mounted() {
    this.$axios
      .get("http://localhost:3003/accounts/" + this.$route.params.homeId)
      .then(res => {
        this.orang = res.data || {};
      });
  }
};
</script>
<style></style>