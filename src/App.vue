<template>
<div class="main">
  <h1 class="main-title">TODO</h1>
  <img class="moon-img" src="./images/icon-moon.svg" alt="">
</div>
  
  <todo-form
  @create="createTodo"
  />
  <todo-list 
  :todos="filteredTodos"
  @remove="removeTodo"
  @update="updateTodo"
  />

  <div class="filters">
    <span class="items-left">{{itemsLeft}} Items left </span>
    <div class="filter-btns">
      <button @click="selected = 'All'" :class="[selected === 'All' ? 'active' : '', 'footer-btn']">All</button>
      <button @click="selected = 'Active'" :class="[selected === 'Active' ? 'active' : '', 'footer-btn']">Active</button>
      <button @click="selected = 'Completed'" :class="[selected === 'Completed' ? 'active' : '', 'footer-btn']">Completed</button>
    </div>
    
    <div>
      <button @click="clearCompleted" class="footer-btn">Clear completed</button>
    </div>
    
  </div>

  <div class="asided">
    <div>
      <button @click="selected = 'All'" :class="[selected === 'All' ? 'active' : '', 'footer-btn']">All</button>
      <button @click="selected = 'Active'" :class="[selected === 'Active' ? 'active' : '', 'footer-btn']">Active</button>
      <button @click="selected = 'Completed'" :class="[selected === 'Completed' ? 'active' : '', 'footer-btn']">Completed</button>
    </div>
  </div>

</template>

<script>

import TodoForm from "@/components/TodoForm"
import TodoList from "@/components/TodoList"

export default {
      components: {
        TodoForm, TodoList
    },
      data() {
        return {
          todos: [],  
          
          categories: [
            {name: 'All', value: 'All'},
            {name: 'Active', value: 'Active'},
            {name: 'Completed', value: 'Completed'},
          ],
          selected: "All"
        }
      },
      computed: {
        itemsLeft() {
          return this.todos.filter(this.inProgress).length
        },
        filteredTodos() {
      if (this.selected === "Completed") {
        return this.todos.filter(el => el.completed)
      }
      if (this.selected === "Active") {
        return this.todos.filter(el => !el.completed)
      }
      return this.todos
    }
  },
      methods: {
        createTodo(todo) {
          if(todo.title.trim() === '') {
            return null
          } else {
            this.todos.push(todo)
          }
         
        },
        removeTodo(todo) {
          this.todos = this.todos.filter(p => p.id !== todo.id)
        },
        updateTodo(todo) {
        const todoIndex = this.todos.findIndex(el => el.id === todo.id)
        this.todos[todoIndex].completed = !this.todos[todoIndex].completed
        },
        inProgress(todo) {
          return !this.isCompleted(todo)
        },
        isCompleted(todo) {
          return todo.completed
        },
        clearCompleted() {
          this.todos = this.todos.filter(this.inProgress)
        },
        updateLocalStorage(){
        localStorage.setItem('todos',JSON.stringify(this.todos))
        }
      },
      watch:{
        todos: {
          handler() {
            this.updateLocalStorage()
          },
          deep: true
      }
  },
  mounted() {
    let todos = localStorage.getItem('todos')
    if (todos){
      this.todos = JSON.parse(todos)
    }
  }
    
  

}
</script>


<style lang="sass">
@import url('https://fonts.googleapis.com/css2?family=Josefin+Sans:wght@400;700&display=swap')

html 
    font-family: 'Josefin Sans', sans-serif
    font-size: 18px

body 
  background-image: url("./images/bg-desktop-light.jpg")
  background-repeat: repeat-x
  display: flex
  justify-content: center
  padding-top: 40px
  margin: 0
  box-sizing: border-box


.main
  display: flex
  align-items: center
  justify-content: space-between

.main-title
  color: white
  font-size: 50px
  letter-spacing: 10px

.filters
  width: 700px
  padding: 18px
  box-sizing: border-box
  background-color: #fff
  border-radius: 8px
  border: 1px solid #ccc
  display: flex
  flex-direction: row
  justify-content: space-between

.footer-btn
  background-color: #fff
  border: none
  outline: 0
  color: #595959
  font-family: 'Josefin Sans', sans-serif
  font-size: 18px
  cursor: pointer
  &:hover
    color: #00ace6

.asided
    display: none

.items-left
  color: #808080

@media screen and (max-width: 375px)
  body 
    background-image: url("./images/bg-mobile-light.jpg") 
    background-repeat: no-repeat
    padding: 20px 50px
  .main
    max-width: 375px
    &-title
      font-size: 40px
  .filters
    width: 320px
  .asided
    display: block
    margin-top: 20px
    width: 320px
    height: 50px
    display: flex
    justify-content: center
    align-items: center
    border-radius: 8px
    border: 1px solid #ccc
  .filter-btns
    display: none
  



@media screen and (min-width: 576px) and (max-width: 768px)
  body
    padding: 40px
    display: flex
    justify-content: center
  .filters
    width: 520px

@media screen and (min-width: 377px) and (max-width: 576px)
  .filters
    width: 350px
  .asided
    display: block
    margin-top: 20px
    width: 350px
    height: 50px
    display: flex
    justify-content: center
    align-items: center
    border-radius: 8px
    border: 1px solid #ccc
  .filter-btns
    display: none
    


</style>