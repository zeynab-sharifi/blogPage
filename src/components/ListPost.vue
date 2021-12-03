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
    </div>
    <!-- loading post -->
    <div class="loader" v-else></div>
</template>
<script>
    import Post from './Post.vue'
    import axios from 'axios'
    import _ from 'underscore';

    export default {
        components:{
            Post
        },
         data(){
            return{
                posts:null,
                loading:false
            }
        },
        created(){
            this.loading = true;
            axios.get('https://jsonplaceholder.typicode.com/posts?_page1&_limit=9')
            .then(res => {
                this.loading=false;
                this.posts = res.data;
                let mainPost = this.posts.shift()

                this.posts = [mainPost , ..._.chunk(this.posts, 2)]
                console.log(this.posts)
            })
            .catch(err => console.log(err))
        }
    }
</script>