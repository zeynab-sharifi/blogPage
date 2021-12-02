<template>
    <post></post>
                <!-- Nested row for non-featured blog posts-->
                <div class="row">
                    <div class="col-lg-6">
                        <post></post>
    <post></post>
                    </div>
                    <div class="col-lg-6">
                        <post></post>
    <post></post>
                    </div>
                </div>
</template>
<script>
    import axios from 'axios'
    import Post from './Post.vue'
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
            axios.get('https://jsonplaceholder.typicode.com/posts?_page1&_limit=9')
            .then(res => console.log(res))
            .catch(err => console.log(err))
        }
    }
</script>