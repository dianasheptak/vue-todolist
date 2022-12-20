<template>
<div>
    <div v-if="todos.length > 0">
        <VueDraggableNext>
        <todo-item 
          v-for="todo in todos"
          :todo="todo"
          :key="todo"
          @remove="$emit('remove', todo)"
          @update="$emit('update', todo)"
          > 
        </todo-item>
        </VueDraggableNext>  
    </div>

    <div v-else class="no-todos">
        You haven't got any tasks 
    </div>
</div>
</template>

<script>
    import TodoItem from "@/components/TodoItem.vue"
    import {VueDraggableNext} from 'vue-draggable-next'
    export default {
     emits: ['remove', 'update'],
     components: { 
        TodoItem, VueDraggableNext
        },
        props: {
            todos: {
                type: Array
            }}}
</script>

<style lang="sass" scoped>
.no-todos
    text-align: center
    color: white
    font-size: 20px
    margin-bottom: 20px

@media screen and (max-width: 379px)
    .no-todos
        color: #9966ff
        padding-top: 30px

</style>