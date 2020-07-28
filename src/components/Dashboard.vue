<template>
  <div class="content" v-if="posts && posts.length">
    <b-row>
      <b-col
        class="col-md-3"
        style="margin-bottom:20px;"
        v-for="post in posts"
        :key="post.source.id"
      >
        <b-card
          :img-src="post.urlToImage"
          img-top
          tag="article"
          style="padding:10dp; text-align:left; width:100%;"
          min-cols="3"
        >
          <b-card-text>
            <p>{{post.title}}</p>
            <br />
            <small>{{post.description}}</small>
          </b-card-text>
          <b-row>
            <b-col class="col-md-12 text-right">
              <b-button :href="post.url" variant="primary">Baca</b-button>
            </b-col>
          </b-row>
        </b-card>
      </b-col>
    </b-row>
  </div>
</template>
<script>
export default {
  name: "Dashboard",
  props: {
    posts:Array,
    errors:Array
  },
};
</script>
<style scoped>
ul {
  text-align: left;
}
.data-body {
  text-align: justify;
}
.content {
  padding: 20px;
  margin: auto;
}
.row > div[class*="col-"] {
  display: flex;
  flex: 1 0 auto;
}
.card-body {
  /* Override default */
  padding: 1rem !important;
}
</style>