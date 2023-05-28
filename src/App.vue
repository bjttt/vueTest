<script setup>
  import { computed } from '@vue/reactivity';
import { ref } from 'vue';
  const blogs=ref([
  {
    id:1,
    title: "First Veu3",
    content:"第一个Veu3程序第一个Veu3程序",
    link:"Veu-3-tutorial",
  },
  {
    id:2,
    title: "second Veu3",
    content:"第er个Veu3程序第er个Veu3程序",
    link:"react-3-tutorial",
  },
  {
    id:3,
    title: "third Veu3",
    content:"第3个Veu3程序第3个Veu3程序",
    link:"javascript-tutorial",
  }])
  const total=computed(() => blogs.value.length)
  const showTotal=ref(true);
  function toggleTotal(){
    showTotal.value=!showTotal.value
  }

  const initialBlogForm ={
    title: "",
    content:"",
    link:"",
  };
  const blogForm=ref({...initialBlogForm});
  function addPost(){
    blogs.value.push({
      id:blogs.value.length+1,
      ...blogForm.value,
    });
    blogForm.value={...initialBlogForm};
  }
</script>

<template>
  <div v-for="blog in blogs" :key="blog.id">
    <h1>
      <a :href="blog.link">{{ blog.title }}</a>
    </h1>
    <article>
      <div>
        {{ blog.content.slice(0,100) }}
      </div>
      <footer v-if="blog.content.length>100">
        <button>阅读原文</button>
      </footer>
    </article>
  </div>
  <h3 v-if = "showTotal">总共{{ total }}篇</h3>
  <button @click="toggleTotal">{{showTotal ? "隐藏":"显示"}}总数</button>
  <form @submit.prevent="addPost">
    <label for="blogTitle">博客标题</label>
    <input type="text" id="blogTitle" v-model="blogForm.title"/>
    <label for="content">内容</label>
    <textarea
      id="content"
      cols="30"
      rows="10"
      v-model="blogForm.content"
      >
    </textarea>
    <label>链接</label>
    <input type="text" id="link" v-model="blogForm.link"/>
    <button type="submit">提交</button>
  </form>
</template>

<style scoped>
form{
  display: grid;
  margin-top: 2em;
}
</style>
