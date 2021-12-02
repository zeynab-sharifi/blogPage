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
import Post from './Post.vue'
export default {
    components:{
        Post
    }
}
</script>