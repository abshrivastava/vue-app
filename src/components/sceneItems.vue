<template>
    <div class="sceneItems mx-1">
        <!-- <p class="sceneItems-Text">{{vueContainer.text}}</p> -->
        <div class="sceneItems-Text"><img class="maxh-60" :src="vueContainer.imgUrl" /></div>
        <div class="sceneItems-Delete"
             @click="deleteItem(vueContainer)"> x
        </div>
    </div>


    
</template>

<script>
// import thumbnail from './assets/thumbnail.png';
     export default {
        name: "vueContainer-item",
        props: ['vueContainer', 'logo'],
        methods: {
            deleteItem(vueContainer) {
                this.$emit('delete', vueContainer)
            }
        }
    }
</script>
<style>
.maxh-60 {
    max-height: 60px;
}


    .sceneItems {
        background-color: white;
        border: 1px solid lightgrey;
        position:relative;
        margin-top: 8px;
        float: left;
    }

    .sceneItems-Text { 
        padding: 10px;
        /* margin-right: 40px; */
    }

    .sceneItems-Delete {
        position: absolute;
        right: 14px;
        top: 9px;
        bottom: 0;
        margin: auto;
        font-size: 18px;
        color: #de4843;
        font-weight: 700;
        cursor: pointer;
    }

</style>