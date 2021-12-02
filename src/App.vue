<script >
import NavBlog from './components/NavBlog.vue'
import HeaderBlog from'./components/lo/HeaderBlog.vue'
import ListPost from './components/ListPost.vue'
import PaginationBlog from './components/lo/PaginationBlog.vue'
import FooterBlog from './components/lo/FooterBlog.vue'
  export default{
    components :{
    NavBlog,
    HeaderBlog,
    ListPost,
    PaginationBlog,
    FooterBlog
}
  }
</script>

<template>
        <!-- Responsive navbar-->
        <nav-blog></nav-blog>
        <!-- header blog page -->
        <header-blog></header-blog>
        <div class="col-lg-12">
                <!-- Featured blog post-->
               <div class="container">
                  <list-post></list-post>
               </div>
                <!-- Pagination-->
                <pagination-blog></pagination-blog>
            </div>
             <!-- Footer-->
            <footer-blog></footer-blog>
</template>

<style>

</style>
