<template>
    <Header />
    <List @toggle-new-todo="toggleNewTodo" :showAddTodo="showNewTodo"/> 
</template>

<script>
import Header from '../components/Header'
import List from '../components/List'


export default {
    name: 'Main',
    components: {
         Header,
         List
    },
    data() {
        return {
        showNewTodo: false,
        }
    },
}
</script>