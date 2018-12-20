<template>
    <div class="storyList">
        <p class="storyList-Text">{{vueContainer.text}}</p>
        <div class="storyList-Delete"
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
    .storyList {
        background-color: white;
        border: 1px solid lightgrey;
        position:relative;
        margin-top: 8px;
    }

    .storyList-Text { 
        padding: 12px;
        margin-right: 40px;
    }

    .storyList-Delete {
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