<template>
  <div v-if="blog" class="container-fluid p-5">
    <div class="row blog-card">
      <div class="col-12">
        <img class="blog-card-img" :src="blog.imgUrl" alt="Blog Image">
      </div>

      <div class="col-12">
        <div class="d-flex mb-3">

          <img :src="blog.creator.picture" :alt="blog.creator.name" class="profile-photo">

          <div class="blog-info">
            <p class="fs-3">{{ blog.title }}</p>
            <div>
              <p class="m-0">By {{ blog.creator.name }}</p>
              <p class="m-0">Last updated: {{ blog.updatedAt.toLocaleDateString() }}</p>
            </div>
          </div>

          <button v-if="loggedInAccount.id == blog.creator.id" class="btn btn-warning edit-profile-button"><i
              class="mdi mdi-pen"></i></button>

        </div>
        <p>{{ blog.body }}</p>
      </div>

    </div>
  </div>
  <div v-else class="container-fluid">
    <h1>Loading. . .</h1>
  </div>
</template>


<script>
import { useRoute } from "vue-router";
import { AppState } from '../AppState';
import { computed, reactive, onMounted } from 'vue';
import Pop from "../utils/Pop";
import { blogsService } from "../services/BlogsService";
export default {
  setup() {
    // VARIABLES
    const route = useRoute()
    const routeBlogId = route.params.blogId
    const blog = computed(() => AppState.activeBlog)
    const loggedInAccount = computed(() => AppState.account)
    // FUNCTIONS
    async function getBlogById() {
      try {
        await blogsService.getBlogById(routeBlogId)
      } catch (error) {
        Pop.error('[ERROR]', error)
      }
    }

    // LIFECYCLE
    onMounted(() => {
      blogsService.resetAllActiveData()
      getBlogById()
    })
    return { blog, loggedInAccount }
  }
};
</script>


<style lang="scss" scoped>
.blog-card-img {
  width: 100%;
  border-radius: 10px;
  margin-bottom: 1em;

}

.profile-photo {
  aspect-ratio: 1 / 1;
  max-width: 20vw;
  border-radius: 50%;
}

.blog-card {
  padding: 2em;
  border-radius: 5px;
  border: solid black 2px;
}

.edit-profile-button {
  width: 5vw;
  height: 5vw;
  font-size: x-large;
}

.blog-info {
  margin-left: 1em;
  margin-right: 1em;
  display: flex;
  flex-direction: column;
  justify-content: space-between;
}
</style>