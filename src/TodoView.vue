<template>
    <hi>ini halaman todo list</hi>

    <form @submit.prevent="todoStore.addTodo(newTodo)">
        <input type="text" v-model="newTodo" placeholder="add new todo...">
        <input type="submit" value="Add">
    </form>

    <div style="width: 500px; padding-inline-start: 40px;">
        <h3 style="text-align: center;">My Todo list</h3>
    </div>

    <div class="getters-button">
        <button @click="show = 'all'">Show All</button>
        <button @click="show = 'done only'">Done Only</button>
        <button @click="show = 'undone only'">Undone Only</button>
    </div>

    <!-- show all todo list -->
    <div v-if="show=='all'">
    <ul>
        <li v-for="list in todoStore.todolist">
            <span>
            {{ list.name }}
            </span>
            <span>
                <button v-fi="!list.isDone" @click="todoStore.setAsDone(list.name)">set as done</button>
                <button v-fi="list.isDone" @click="todoStore.setAsUnDone(list.name)">set as undone</button>
            </span>
        </li>
    </ul>
</div>

<!-- show done only todo list-->
 <div v-if="show=='done only'">
    <ul>
        <li v-for="list in todoStore.doneOnly">
            <span>
                {{ list.name }}
            </span>
            <span>
                <button v-if="!list.isDone" @click="todoStore.setAsDone(list.name)">set as done</button>
                <button v-if="list.isDone" @click="todoStore.setAsDone(list.name)">set as undone</button>
            </span>
        </li>
    </ul>
 </div>

    <!-- show undone only todo list -->
     <div v-if="show=='undone only'">
        <ul>
        <li v-for="list in todoStore.undoneOnly">
            <span>
                {{ list.name }}
            </span>
            <span>
                <button v-if="!list.isDone" @click="todoStore.setAsDone(list.name)">set as done</button>
                <button v-if="list.isDone" @click="todoStore.setAsDone(list.name)">set as undone</button>
            </span>
        </li>
    </ul>
 </div>
</template>
<style scoped>
form {
    width: 500px;
    padding-inline-start: 40px;
    margin-bottom: 40px;
}

form input {
    padding: 10px;
}

form input:first-child {
    width: 80%;
    margin: 0px 10px;
}
    ul {
        list-style: none;
        width: 500px;
    }
    li {
        border: solid 1px;
        margin: 10px;
        padding: 10px;
        display: flex;
        justify-content: space-between;
    }

.getters-button {
    display: flex;
    justify-content: center;
    gap: 10px;
    width: 500px; 
    padding-inline-start: 40px;
}

</style>

<script>
import { useTodoStrore } from './stores/todoStore';

export default {
    setup() {
        const todoStore = useTodoStore()

        return { todoStore }
    },
    data() {
        return {
            newTodo: '',
            show: 'all'
        }
    }
}
</script>