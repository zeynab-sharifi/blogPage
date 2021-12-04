<script >
  import NavBlog from './components/NavBlog.vue'
  import HeaderBlog from'./components/layouts/HeaderBlog.vue'
  import ListPost from './components/ListPost.vue'
  import FooterBlog from './components/layouts/FooterBlog.vue'
    export default{
      components :{
      NavBlog,
      HeaderBlog,
      ListPost,
      FooterBlog
  },
 
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
                
            </div>
             <!-- Footer-->
            <footer-blog></footer-blog>
</template>

<style>

</style>
