<template>
    <nav aria-label="Pagination">
                    <hr class="my-0" />
                    <ul class="pagination justify-content-center my-4">
                        <li class="page-item" :class="{'disabled' : fristPage}">
                            <button type="button" class="page-link" :disabled="fristPage">Newer</button>
                        </li>
                        
                        <li class="page-item active" v-for="page in pages" :key="page.name" :class="{'active' :page.activePages}">
                            <button class="page-link" :disabled="page.activePages">{{ page.name }}</button>
                        </li>
                        

                        <li class="page-item"  :class="{'disabled' : lastPage}">
                            <button type="button" class="page-link" :disabled="lastPage">Older</button>
                        </li>
                    </ul>
                </nav>
</template>
<script>
export default {
    props:{
        totalPage : {
            type : Number,
            required : true
        },
        // prePage : {
        //     type : Number,
        //     required : true
        // },
        currentPage : {
            type : Number,
            required : true
        }
    },
    computed:{
        pages(){
            let range = [];
            for(let i=1; i<= this.totalPage;i++){
                range.push({
                    name: i,
                    activePages : i===this.currentPage
                })
            }
            return range;
        },
        fristPage(){
            return this.currentPage === 1;
        },
        lastPage(){
             return this.currentPage === this.totalPage;
        }

    }
}
</script>