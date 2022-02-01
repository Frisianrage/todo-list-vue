<template>
    <div class="item">
        <h3 :class="{done: item.done }">
            {{item.name}}
            <div class="icons">
                <i @click="$emit('itemDone', item.id)" class="far fa-check-circle"></i>
                <i @click="$emit('deleteTodo', item.id)" class="far fa-trash-alt"></i>
            </div>
        </h3> 
    </div> 
</template>

<script>
export default {
    name: 'Todo',
    props: {
        item: Object
        }
}

</script>

<style scoped>

.item {
  background: #f4f4f4;
  margin: 5px;
  padding: 10px 20px;
  
}

.done {
    text-decoration: line-through;
}

.far {
    padding-right: 10px;
    cursor: pointer;
}

.task.reminder {
  border-left: 5px solid green;
}

.item h3 {
  display: flex;
  align-items: center;
  justify-content: space-between;
}
</style>