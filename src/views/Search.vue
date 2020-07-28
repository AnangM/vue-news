<template>
  <div class="search">
    <b-row>
      <b-col class="md-12 text-center">
        <b-form-input
          v-on:keydown.enter="fetchData()"
          v-model="query"
          class="search-bar d-inline"
          placeholder="Search"
        ></b-form-input>
        <b-button
          variant="primary"
          class="d-inline"
          style="margin-left:10px;"
          @click="fetchData()"
        >Search</b-button>
      </b-col>
    </b-row>
    <dashboard :posts="posts" :errors="errors"/>
  </div>
</template>

<script>
// @ is an alias to /src
import Dashboard from "@/components/Dashboard.vue";

export default {
  name: "Search",
  components: {
    Dashboard,
  },
  data() {
    return {
      query: "",
      posts : [],
      errors : []
    };
  },
  created() {
    this.fetchData();
  },
  methods: {
    async fetchData() {
      var q = "";
      if (this.query != null || this.query != undefined) {
        q = this.query;
      }
      await this.axios({
        method: "get",
        url: `https://newsapi.org/v2/top-headlines?q=${q}&category=technology&apiKey=9cf026c392f94f2488d8165b776512e2`,
      })
        .then((response) => {
          if(response.data.totalResults > 0){
              this.posts = response.data.articles;
          }else{
              alert("No Data!")
          }
        })
        .catch((e) => {
          this.errors.push(e);
        });
    },
  },
};
</script>
<style scoped>
.search {
  padding: 20px;
}
.search-bar {
  max-width: 800px;
}
</style>
