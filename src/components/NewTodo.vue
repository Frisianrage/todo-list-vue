<template>
    <form @submit="onSubmit">
        <div>
            <input type="text" v-model='name' name='name' placeholder="Enter new to do" />       
        </div>
        <input type="submit" value="Add" class="button" />
    </form>
</template>


<script>
export default {
    name: "NewTodo",
    data() {
        return {
        name: '',
        done: false,
        }
    },
    methods: {
        onSubmit(e) {
        e.preventDefault()

        if (!this.name) {
        alert('Please add a to-do')
        return
        }

        const newTodo = {
        id: Math.floor(Math.random() * 100000),
        name: this.name,
        done: this.done
        }

        this.$emit('add-todo', newTodo)

        this.name = ''

        },
    }
    
}
</script>


<style>
    input {
        width: 80%;
        font-size: 20px;
        padding: 5px;
        margin: 15px 0
    }
    button {
        margin-top: 15px;
        margin-bottom: 15px;
        padding-left: 20px;
        padding-right: 20px;
        border-radius: 20px;
        background-color: green;
        color: #fff;
        font-size: 16px;
        font-weight: 700;
    }
</style>