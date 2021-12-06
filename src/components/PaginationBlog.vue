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
import { computed, toRefs } from "vue"; 
export default {
    props:{
        totalPage : {
            type : Number,
            required : true
        },
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
    setup(props , context){
        const {currentPage , totalPage , maxVisibleBtn } = toRefs(props);
    //pagination start button
        const startPage = computed(()=>{
            if(currentPage.value ===1) return 1;


            if(currentPage.value === totalPage.value) return totalPage.value -5;

            return currentPage.value -2;
        })
    //pagination end page
        const endPage = computed(() => Math.min(startPage.value + maxVisibleBtn.value-1, totalPage.value))

        const pages = computed(()=>{
            let range = [];
            for(let i=startPage.value; i <= endPage.value;i++){
                range.push({
                    name: i,
                    activePages : i==currentPage.value
                })
            }
            return range; 
        })

        const fristPage = computed(()=>{currentPage.value === 1})

        const lastPage = computed(()=>{currentPage.value === totalPage.value})

        function clickPage(page){
            context.emit('pagechange', page)
        }

        return {
            pages,
            fristPage,
            lastPage,
            clickPage
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