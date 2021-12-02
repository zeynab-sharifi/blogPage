<template>
<!-- loading post -->
    <div v-if="!loading">
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
    </div>
    <!-- loading post -->
    <div class="loader" v-else></div>
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
            this.loading = true;
            axios.get('https://jsonplaceholder.typicode.com/posts?_page1&_limit=9')
            .then(res => {
                this.loading=false;
                console.log(res.data)
            })
            .catch(err => console.log(err))
        }
    }
</script>