<template>
    <div>
        <h3>{{todo_title}}</h3>
        <table>
            <tr>
                <th>Index</th>
                <th>Title</th>
                <th>Important</th>
                <th>Completed</th>
            </tr>
            <tr v-for="(todo, i) in todos" v-bind:key="i">
                <th>{{i}}</th>
                <th>{{todo.title}}</th>
                <th>{{todo.important ? 'Yes' : 'No'}}</th>
                <th><input type="checkbox" v-model="todo.completed"></th>
            </tr>
        </table>
        <hr/>
        TODO: <input type="text" v-model="title"><br>
        IMPORTANT: <input type="checkbox" v-model="important"><br>
        <button @click="createTodo">Create Todo</button>
    </div>
</template>

<script>
export default {
    props: {todo_title : String},
    data: function() {
        return {
            todos:[],
            title: '',
            important: false
        }
    },
    created: function() {
        console.log(this.todos);
    },
    methods: {
        createTodo() {
            if (!this.title) {
                alert('todoに何も書いてません');
            } else {
                var new_todo = {title: this.title, important: this.important, completed: false}
                this.todos.push(new_todo);
            }
        }
    }
}
</script>

<style>
</style>