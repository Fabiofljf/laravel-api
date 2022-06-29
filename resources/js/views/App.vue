<template>
  <main id="site_main">
    <WorkInProgress />
    <div class="container">
      <div class="row">
        <div class="col-10 d-flex flex-wrap">
          <div class="col p-3" v-for="post in posts" :key="post.id">
            <div class="card text-start">
              <img
                class="card-img-top"
                :src="post.cover_images"
                alt="post.title"
              />
              <div class="card-body">
                <h4 class="card-title">{{ post.title }}</h4>
                <p class="card-text">{{ 'trimText(post.content)' }}</p>
              </div>
            </div>
          </div>
          <!-- /.col Posts-->
        </div>
        <!-- /.col sx-->
        <div class="col">
          <div class="col">
            <h4 class="p-2"><strong>Categories:</strong></h4>
            <ul v-for="category in categories" :key="category.id">
              <li>{{category.name}}</li>
            </ul>
          </div>
          <!-- /.col Tags-->
          <div class="col mt-4">
            <h4 class="p-2"><strong>Tags:</strong></h4>
            <ul v-for="tag in tags" :key="tag.id">
              <li class="btn btn-primary">{{tag.name}}</li>
            </ul>
          </div>
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
      categories: "",
      tags: "",
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
        })
        .catch((e) => {
          console.error(e);
        });
    },
    trimText(text) {
      if (text.length > 100) {
        return text.slide(0, 100);
      }
      return text;
    },
    getCallCategories() {
      axios
        .get("/api/categories")
        .then((response) => {
          this.categories = response.data;
        })
        .catch((e) => {
          console.error(e);
        });
    },
    getCallTags() {
      axios
        .get("/api/tags")
        .then((response) => {
          this.tags = response.data;
        })
        .catch((e) => {
          console.error(e);
        });
    },
  },
  mounted() {
    this.getCallPosts();
    this.getCallCategories();
    this.getCallTags();
  },
};
</script>
