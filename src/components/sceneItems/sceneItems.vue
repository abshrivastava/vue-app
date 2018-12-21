<!-- Stylesheet -->
<style src="./sceneItems.css"></style>

<!-- HTML Layout -->
<template lang="html" src="./sceneItems.html"></template>

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
