<template>
    <div class="ToDoItem">
        <p class="ToDoItem-Text">{{todo.text}}</p>
        <div class="ToDoItem-Delete"
             @click="deleteItem(todo)"> x
        </div>
    </div>
</template>

<script>
    export default {
        name: "to-do-item",
        props: ['todo'],
        methods: {
            deleteItem(todo) {
                this.$emit('delete', todo)
            }
        }
    }
</script>
<style>
    .ToDoItem {
        background-color: white;
        border: 1px solid lightgrey;
        position:relative;
        margin-top: 8px;
    }

    .ToDoItem-Text { 
        padding: 12px;
        margin-right: 40px;
    }

    .ToDoItem-Delete {
        position: absolute;
        right: 14px;
        top: 9px;
        width: 30px;
        bottom: 0;
        margin: auto;
        font-size: 18px;
        color: #de4843;
        font-weight: 700;
        cursor: pointer;
        text-align: center;
    }

</style>