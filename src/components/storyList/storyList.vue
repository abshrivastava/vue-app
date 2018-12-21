<!-- Stylesheet -->
<style src="./storyList.css"></style>

<!-- HTML Layout -->
<template lang="html" src="./storyList.html"></template>

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
