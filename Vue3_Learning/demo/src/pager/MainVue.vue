<template>
  <div class="main">
      <h3>MainVue</h3>
      <ArticleVue/>
      <ArticleVue/>
  </div>
</template>

<script>
import ArticleVue from "@/pager/ArticleVue.vue";
export default {
  components:{
      ArticleVue,
  }
}
</script>

<style scoped>
.main{
    float: left;
    width: 70%;
    height: 600px;
    border: 5px solid #999;
    box-sizing: border-box;
}
</style>