<template>
  <PostForm :post="post" :submitForm="createPost" />
</template>

<script>
import PostForm from "../components/PostForm.vue";
import { useRouter } from "vue-router";
import { reactive } from "vue";
export default {
  components: {
    PostForm,
  },
  setup() {
    const API_URL = "https://blogapiexpresswithvue.herokuapp.com/posts";
    const router = useRouter();

    const post = reactive({
      title: "",
      content: "",
      creator: "",
    });

    async function createPost() {
      const response = await fetch(API_URL, {
        method: "POST",
        headers: {
          "content-type": "application/json",
        },
        body: JSON.stringify({
          title: post.title,
          content: post.content,
          creator: post.creator,
        }),
      });
      const json = await response.json();
      router.push({
        name: "Home",
      });
    }

    return {
      post,
      createPost,
    };
  },
};
</script>

<style></style>
