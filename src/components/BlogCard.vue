<template>
  <router-link :to="{ name: 'BlogDetails', params: { blogId: blog.id } }">
    <div class="container-fluid selectable text-black">
      <div class="row blog-card">

        <div class="col-8">
          <div class="d-flex flex-column justify-content-between">
            <div class="d-flex align-items-center">
              <img :src="blog.creator.picture" :alt="blog.creator.name" class="profile-photo">
              <p class="m-0 ms-2">{{ blog.creator.name }}</p>
            </div>
            <p class="fw-bold">{{ blog.title }}</p>
            <p>{{ blog.body.substring(0, 140) }}<span v-if="blog.body.length > 140">. . .</span></p>
          </div>
          <p>{{ blog.updatedAt.toLocaleDateString() }}</p>
        </div>

        <div class="col-4">
          <img class="blog-card-img" :src="blog.imgUrl" alt="Blog Image">
        </div>

      </div>
    </div>
  </router-link>
</template>


<script>
import { AppState } from '../AppState';
import { computed, reactive, onMounted } from 'vue';
import { Blog } from "../models/Blog";
export default {
  props: {
    blog: { type: Blog, required: true }
  },
  setup() {
    return {}
  }
};
</script>


<style lang="scss" scoped>
.blog-card-img {
  width: 100%;
  height: 25vh;
  object-fit: cover;
  object-position: center;
  border-radius: 5px;
}

.blog-card {
  padding-top: .6em;
  padding-bottom: .6em;
  border-radius: 5px;
  border: solid black 2px;
}

.profile-photo {
  aspect-ratio: 1 / 1;
  max-width: 4vw;
  border-radius: 50%;
}
</style>