<template>
    <div class="sceneItems mx-1">
        <!-- <p class="sceneItems-Text">{{vueContainer.text}}</p> -->
        <p class="sceneItems-Text"><img src={vueContainer.logo} /></p>
        <div class="sceneItems-Delete"
             @click="deleteItem(vueContainer)"> x
        </div>
    </div>
</template>

<script>
     export default {
        name: "vueContainer-item",
        props: ['vueContainer'],
        methods: {
            deleteItem(vueContainer) {
                this.$emit('delete', vueContainer)
            }
        }
    }
</script>
<style>
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