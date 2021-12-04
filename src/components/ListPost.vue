<template>
<!-- loading post -->
    <div v-if="!loading">
        <post :post="posts[0]"></post>
        <!-- Nested row for non-featured blog posts-->
            <div class="row">
                <div class="col-lg-6" v-for="(postGroup , index) in posts.slice(1)" :key="index">
                    <post v-for="post in postGroup" :key="post.id" :post="post"></post>
                    
                </div>
            </div>
               <!-- Pagination-->
                <pagination-blog :currentPage="page.current" :totalPage="page.totalPage" @pagechange="changepage"></pagination-blog>

    </div>
    <!-- loading post -->
    <div class="loader" v-else></div>
</template>
<script>
    import Post from './Post.vue'
    import axios from 'axios'
    import _ from 'underscore';
    import PaginationBlog from './PaginationBlog.vue';

    export default {
        components:{
            Post,
            PaginationBlog
        },
         data(){
            return{
                posts:null,
                loading:false,
                page:{
                    current : 1,
                    totalPage : 0
                }
            }
        },
         methods :{
            changepage(page){
                this.getPostData(page)
            },
            getPostData(page = 1){      
            this.loading = true;
            axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${page}&_limit=9`)
            .then(res => {
                this.loading=false;
                this.posts = res.data;
                let mainPost = this.posts.shift()

                this.posts = [mainPost , ..._.chunk(this.posts, 2)]
                this.page.current = page;
                this.page.totalPage= parseInt(parseInt(res.headers['x-total-count']/9))
                // console.log(this.page)
            })
            .catch(err => console.log(err))
        
            }
        },
        created(){
            this.getPostData(1)
        }
    }
</script>