<template>
    <nav aria-label="Pagination">
                    <hr class="my-0" />
                    <ul class="pagination justify-content-center my-4">
                        <li class="page-item" :class="{'disabled' : fristPage}">
                            <button type="button" class="page-link" :disabled="fristPage" @click="clickPage(1)">Newer</button>
                        </li>
                        
                        <li class="page-item" v-for="page in pages" :key="page.name" :class="{'active' :page.activePages}">
                            <button type="button" class="page-link" @click="clickPage(page.name)" :disabled="page.activePages">{{ page.name }}</button>
                        </li>
                        

                        <li class="page-item"  :class="{'disabled' : lastPage}">
                            <button type="button" class="page-link" :disabled="lastPage" @click="clickPage(totalPage)">Older</button>
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
        },
        maxVisibleBtn :{
            type:Number,
            required: false,
            default:5
        }
    },
    computed:{
        //pagination start button
        startPage(){
            if(this.currentPage ===1)return 1;


            if(this.currentPage === this.totalPage) return this.totalPage -5;

            return this.currentPage -2;
        },
        //pagination end page
        endPage(){
            return Math.min(this.startPage + this.maxVisibleBtn-1, this.totalPage);
        },
        pages(){
            let range = [];
            for(let i=this.startPage; i <= this.endPage;i++){
                range.push({
                    name: i,
                    activePages : i==this.currentPage
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

    },
    methods:{
        clickPage(page){
            // console.log(page)
            this.$emit('pagechange' , page)
        }
    }
}
</script>
<style lang="scss" scoped>
    .pagination .page-link{
        border: none;
        margin: 0 5px;
    }
    .pagination .page-item.active .page-link{
        background-color: #eb4d4b;
        border-radius: 7px;
        color: #fff;
        box-shadow: 0 1px 2px rgba(0,0,0,.12);
    }
    .pagination .page-item .page-link{
        color: #eb4d4b;
    }
    .page-link:hover{
        color: #121212;
        border-radius: 7px;
    }
</style>