<template>
    <div class="container">
        <div class="head">
            <h3>These are your to-dos!</h3>
            <button @click="toggleNewTodo" >Add new To Do</button>
        </div>
        <div v-show="showNewTodo" class="newtodo">
            <NewTodo @add-todo="addTodo" /> 
        </div>
         
        <div :key="item.id" v-for="item in itemList">
            <Todo :item="item" @deleteTodo="deleteTodo" @itemDone="itemDone" />
        </div>
    </div>
</template>


<script>
import Todo from './Todo'
import NewTodo from './NewTodo'

export default {
    name: 'List',
    components: {
        Todo,
        NewTodo
    },
    data() {
        return {
        itemList: [],
        showNewTodo: false
         }       
        },    
    methods: {
        toggleNewTodo() {
        this.showNewTodo = !this.showNewTodo
        },
        async addTodo(item) {
            const res = await fetch('http://localhost:3000/items', {
                method: 'POST',
                headers: {
                'Content-type': 'application/json',
                },
                body: JSON.stringify(item),
            })

            const data = await res.json()

            this.itemList = [...this.itemList, data]
        },
        async getItems() {
            const res = await fetch('http://localhost:3000/items')
            const data = res.json()
            
            return data
        },
        async deleteTodo(id) {
            const res = await fetch(`http://localhost:3000/items/${id}`, {
                method: 'DELETE'
            })

           res.status === 200
          ? (this.itemList = this.itemList.filter((item) => item.id !== id))
          : alert('Error deleting task')
        },
        async getItem(id) {
            const res = await fetch(`http://localhost:3000/items/${id}`)
            const data = await res.json()

            return data
        },
        async itemDone(id) {
            const item = await this.getItem(id)

            const isDone = {...item, done: !item.done}

            const res = await fetch(`http://localhost:3000/items/${id}`, {
                method: 'PUT',
                headers: {
                    'Content-type': 'application/json',
                },
                body: JSON.stringify(isDone)
            })

            const data = await res.json()
            
            this.itemList = this.itemList.map((item) =>
            item.id === id ? { ...item, done: data.done } : item)
        }
    },
    async created() {
        this.itemList = await this.getItems()
    },
}
</script>


<style scoped>
    .container {
        margin: 30px auto;
        border: 2px solid red;
        width: 60%;
    }
    .head {
        display: flex;
        justify-content: space-evenly;
    }
    .newtodo {
        text-align: center
    }
     button {
        align-items: center;
        margin-top: 15px;
        margin-bottom: 15px;
        padding-left: 20px;
        padding-right: 20px;
        border-radius: 20px;
        background-color: blue;
        color: #fff;
        font-size: 16px;
        font-weight: 700;
        cursor: pointer;
    }
</style>