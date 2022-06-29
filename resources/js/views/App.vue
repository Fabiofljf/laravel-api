<template>
  <main id="site_main">
    <WorkInProgress />
    <div class="container">
      <div class="row">
        <div class="col-10 d-flex flex-wrap">
          <div class="col g-3" v-for="post in posts" :key="post.id">
            <div class="card text-start">
              <img
                class="card-img-top"
                :src="post.cover_images"
                alt="post.title"
              />
              <div class="card-body">
                <h4 class="card-title">{{ post.title }}</h4>
                <p class="card-text">{{ post.content }}</p>
              </div>
            </div>
          </div>
          <!-- /.col Posts-->
        </div>
        <!-- /.col sx-->
        <div class="col">
          <div class="col"></div>
          <!-- /.col Tags-->
          <div class="col"></div>
          <!-- /.col Categories-->
        </div>
        <!-- /.col dx-->
      </div>
    </div>
  </main>
</template>


<script>
import WorkInProgress from "../components/WorkInProgress";
export default {
  name: "App",
  components: {
    WorkInProgress,
  },
  data() {
    return {
      posts: "",
    };
  },
  methods: {
    getCallPosts() {
      axios
      .get("/api/posts")
      .then((response) => {
        //console.log(response);
        //console.log(response.data);
        this.posts = response.data;
      });
    },
  },
  mounted() {
    this.getCallPosts();
  },
};
</script>
