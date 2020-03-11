<template>
  <div>
    <h1>Data List</h1>
    <nuxt-link to="/data/create">
      <button>tambah data</button>
    </nuxt-link>
    <b-form-input type="text" v-model="cari" placeholder="cari disini"></b-form-input>
    <!-- <b-button variant="primary" @click="submit">Search</b-button> -->
    <p v-if="isError">error</p>
    <p v-else-if="isEmpty">tidak ditemukan</p>
    <table v-else-if="!isLoading" border="1 solid">
      <thead>
        <tr>
          <th>ID</th>
          <th>Title</th>
          <th>isi body</th>
          <th>userID</th>
          <th>action</th>
        </tr>
      </thead>
      <tbody>
        <ListItem
          v-for="data in datas"
          :id="String(data.id)"
          :key="String(data.id)"
          :title="data.title"
          :body="data.body"
          :userId="String(data.userId)"
          @refresh-dong="getData"
        ></ListItem>
      </tbody>
    </table>
    <b-spinner v-else label="Spinning"></b-spinner>
    <!-- <b-table striped hover :items="datas"></b-table> -->
  </div>
</template>

<script>
import Axios from "axios";
import ListItem from "~/components/list-item";

export default {
  components: { ListItem },
  data() {
    return {
      datas: [],
      isError: false,
      isEmpty: false,
      isLoading: false,
      cari: ""
    };
  },
  mounted() {
    this.getData();
  },
  methods: {
    //   submit: function(){
    //       this.getCari()
    //   },
    //   nyari: function(){
    //       cari = this.isicari
    //   },
    async getData() {
      this.isLoading = true;

      try {
        const res = await Axios.get("http://localhost:3001/datas");
        this.datas = res.data;

        if (this.datas.length === 0) {
          this.isEmpty = true;
        }
      } catch (err) {
        console.error(err);

        this.isError = true;
      }

      this.isLoading = false;

      // STYLE JADUL
      // Axios.get('https://jsonplaceholder.typicode.com/datas')
      //   .then((res) => {
      //     this.datas = res.data

      //     if (this.datas.length === 0) {
      //       this.isEmpty = true
      //     }

      //     this.isLoading = false
      //   })
      //   .catch((err) => {
      //     console.error(err)

      //     this.isError = true
      //     this.isLoading = false
      //   })
    },
    // kode muklas
    // computed:{
    //     filteredPosts: function(){
    //         return this.posts.filter((post) => {
    //             return post.title.match(this.cari);
    //         });
    //     },
    // }

    getCari() {
      this.$axios
        .get("http://localhost:3001/datas/?q=" + this.cari)
        .then(() => {
          this.$emit("");
        });
    }
  }
};
</script>

<style scoped></style>