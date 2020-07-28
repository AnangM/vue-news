<template>
  <div class="home">
    <dashboard :posts="posts" :errors="errors" />
  </div>
</template>

<script>
// @ is an alias to /src
import Dashboard from "@/components/Dashboard.vue";

export default {
  name: "Home",
  components: {
    Dashboard,
  },
  data() {
    return {
      posts: [],
      errors: [],
    };
  },
  async created() {
    await this.axios({
      method: "get",
      url: `https://newsapi.org/v2/top-headlines?category=technology&apiKey=9cf026c392f94f2488d8165b776512e2`,
    })
      .then((response) => {
        // JSON responses are automatically parsed.
        this.posts = response.data.articles;
      })
      .catch((e) => {
        this.errors.push(e);
      });
  },
};
</script>
