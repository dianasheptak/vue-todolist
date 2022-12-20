<template>
    <div>
        <div 
        class="todo-item"
        :key="todo.id" > 
        
        <div class="first-block">
            <div class="wrapper" v-if="!todo.completed">
                <button @click="$emit('update', todo)" v-if="!todo.completed" class="not-done "></button>
                <div class="text">{{ todo.title }}</div>
            </div>

            <div class="wrapper" v-else>
                <button @click="$emit('update', todo)" class="on-done toggle-completed">
                    <img src="../images/icon-check.svg" alt=""></button>
                 <div class="text-done text">{{ todo.title }}</div>
            </div>
      </div>
        
        <button 
            @click="$emit('remove', todo)"
            class="delete-btn">
            <img src="../images/icon-cross.svg" 
            alt="delete-cross img">
        </button>
        </div> 
    </div>
</template>

<script>
    export default {
        props: {
            todo: {
                type: Object,
                required: true
            }
        },
         methods: {
        toggleTodo() {
        console.log(this.todo)
    }
  }
    }
</script>

<style lang="sass" scoped>
.todo-item 
    background-color: #fff
    width: 700px
    height: 60px
    border: 1px solid #ccc
    border-radius: 5px
    font-family: 'Josefin Sans', sans-serif
    font-size: 18px
    display: flex
    align-items: center
    flex-direction: row
    justify-content: space-between
    color: #595959
    padding: 0 20px
    outline: 0
    box-sizing: border-box

.wrapper
  display: flex
  gap: 30px
    
.text
    padding-top: 12px
    cursor: pointer

.text-done
    padding-top: 12px
    color: #ccc
    text-decoration: line-through

.first-block
    display: flex
    flex-direction: row
    gap: 30px
    
    
.on-done, .not-done 
    width: 40px
    height: 40px
    border-radius: 50%
    border: 1px solid #ccc
    cursor: pointer
    background: linear-gradient(to right, #47DAFF, #C058F3)

.not-done
    background: #fff

.on-done
    color: #ff8080

.toggle-completed
    text-decoration: line-through
    
.delete-btn
    background-color: #fff
    border: none
    outline: 0
    cursor: pointer

@media screen and (max-width: 375px)
    .todo-item
        width: 320px
    .on-done, .not-done 
        width: 32px
        height: 32px
    .first-block
        gap: 20px

@media screen and (min-width: 376px) and (max-width: 575px)
    .todo-item
        width: 350px
        height: 50px
    .on-done, .not-done 
        width: 32px
        height: 32px
    .first-block
        gap: 20px


@media screen and (min-width: 576px) and (max-width: 768px)
    .todo-item
        width: 520px
    .on-done, .not-done 
        width: 32px
        height: 32px
    .first-block
        gap: 20px
</style>