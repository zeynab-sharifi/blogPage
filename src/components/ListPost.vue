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
    import { ref , reactive} from 'vue'
    import Post from './Post.vue'
    import axios from 'axios'
    import _ from 'underscore';
    import PaginationBlog from './PaginationBlog.vue';

    export default {
        components:{
            Post,
            PaginationBlog
        },
        setup(){
            const posts = ref([]);
            const loading = ref(false);
            const page = reactive({
                    current : 1,
                    totalPage : 0
                })

            function getPostData(pageNumber = 1){      
            loading.value = true;
            axios.get(`https://jsonplaceholder.typicode.com/posts?_page=${pageNumber}&_limit=9`)
            .then(res => {
                loading.value = false;
                posts.value = res.data;
                let mainPost = posts.value.shift()

                posts.value = [mainPost , ..._.chunk(posts.value, 2)]
                page.current = pageNumber;
                page.totalPage= parseInt(parseInt(res.headers['x-total-count']/9))
                console.log(posts,pageNumber)
            })
            .catch(err => console.log(err))
        
            }

            function changepage(page = 1){
                getPostData(page);
            }

            getPostData(1);

            return {
                posts,
                loading,
                page,
                changepage
            }
        },
        
    }
</script>