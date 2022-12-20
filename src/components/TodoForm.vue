<template>
<span class="circle"></span>
    <form @submit.prevent>
      <input 
          class="add-input"
          type="text"
          placeholder="Create a todo..."
          v-model.trim="todo.title"
          @change="createTodo"
        >
    </form>
</template>

<script>
    export default {
        data() {
            return {
                todo: {
                    title: ''
                }
            }
        },
        methods: {
            createTodo() {
          this.todo.id = Date.now()
          this.todo.completed = false
          this.$emit('create', this.todo)
          this.todo = {
            title: '',
          }},
        }
    }
</script>

<style lang="sass" scoped>
.add-input
    padding: 0
    width: 700px
    height: 60px
    border: 1px solid #ccc
    border-radius: 5px
    font-family: 'Josefin Sans', sans-serif
    font-size: 18px
    color: #595959
    padding-left: 75px
    outline: 0
    margin-bottom: 40px
    box-sizing: border-box

.circle
    display: block
    background-color: #fff
    position: absolute
    width: 40px
    height: 40px
    border-radius: 50%
    margin-top: 10px
    margin-left: 15px
    border: 1px solid #ccc
    

@media screen and (max-width: 375px)
    .add-input
        width: 320px
        margin-bottom: 20px
        padding-left: 65px
    .circle
        position: absolute
        width: 32px
        height: 32px
        top: 116px
        margin-left: 15px

@media screen and (min-width: 376px) and (max-width: 575px)
    .add-input
        width: 350px
        height: 50px
        margin-bottom: 30px
        padding-left: 65px
    .circle
        position: absolute
        width: 32px
        height: 32px
        margin-top: 8px
        margin-left: 15px

@media screen and (min-width: 576px) and (max-width: 768px)
    .add-input
        width: 520px
        padding-left: 70px
    .circle
        position: absolute
        width: 36px
        height: 36px
        top: 158px
        margin-left: 15px


</style>