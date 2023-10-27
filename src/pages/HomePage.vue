<template>
  <div class="container-fluid">
    <div class="row px-5">
      <div v-for="blog in blogs" :key="blog.id" class="col-12 pt-5">
        <BlogCard :blog="blog" />
      </div>
    </div>
  </div>
</template>


<script>
import { AppState } from '../AppState';
import { computed, reactive, onMounted } from 'vue';
import Pop from "../utils/Pop";
import { blogsService } from '../services/BlogsService.js'
export default {
  setup() {
    // VARIABLES
    const blogs = computed(() => AppState.blogs)

    // FUNCTIONS
    async function getBlogs() {
      try {
        await blogsService.getBlogs()
      } catch (error) {
        Pop.error("[ERROR]", error)
      }
    }

    // LIFECYCLE / LISTENER FUNCTIONS
    onMounted(() => {
      getBlogs()

    })


    // RETURN
    return { blogs }
  }
};
</script>


<style lang="scss" scoped></style>