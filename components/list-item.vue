<template>
  <tr>
    <td>{{ id }}</td>
    <td>{{ title }}</td>
    <td>{{ body }}</td>
    <td>{{ userId }}</td>
    <td>
      <nuxt-link :to="'/data/' + id">view</nuxt-link>,
      <nuxt-link :to="'/data/' + id + '/edit'">edit</nuxt-link>,
      <button @click="hapus">delete</button>
    </td>
  </tr>
</template>

<script>
export default {
  props: {
    id: {
      type: String,
      default: ""
    },
    title: {
      type: String,
      default: ""
    },
    body: {
      type: String,
      default: ""
    },
    userId: {
      type: String,
      default: ""
    }
  },
  methods: {
    hapus() {
      const setuju = confirm("Data akan dihapus secara permanen..");
      if (!setuju) {
        return;
      }
      const setuju2 = confirm("Apakah Anda yakin?");
      if (!setuju2) {
        return;
      }

      this.$axios.delete("http://localhost:3001/datas/" + this.id).then(() => {
        this.$emit("refresh-dong");
      });
    }
  }
};
</script>

<style></style>
