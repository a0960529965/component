<template>
    <div class="info">
        <h2>Todo List:</h2>
        <div>
            <!-- 加一個 input 用來新增 todo
        希望按 enter 也可以增加 todo
        在 Vue 裡面要捕捉 "按鍵事件" 可以使用 @keyup.[鍵位碼]
        加入 @keyup.enter(修飾) 也等於 @keyup.13-->
            <input type="text" placeholder="add Todo.." v-model="newTodo" @keyup.enter="actionAddTodo" />
            <!-- 按鈕增加 todo -->
            <button @click="actionAddTodo">add todo</button>
        </div>
        <ul>
            <!-- 使用 for render todos -->
            <li v-for="(todo, index) in todos" :key="index">
                <!--  提取 content 顯示 -->
                {{ todo.content }}
            </li>
        </ul>
    </div>
</template>

<script>
    import { mapGetters } from 'vuex'
    export default {
        name: 'info',
        data() {
            return {
                newTodo: ''
            }
        },
        computed: mapGetters({
            // 使用取 list 的函式，將資料存在 todos
            todos: 'getTodos',
        }),
        methods: {
            actionAddTodo() {
                // 方法一、使用
                // this.addTodo( this.newTodo );
                // 這邊示範第二種方法，不需要先引入 action 可以直接呼叫（調用）。
                // 使用 this.$store.dispatch( action(String), value );
                this.$store.dispatch('addTodo', this.newTodo);
                // 清除 data 中 input 的 value
                this.newTodo = '';
            }
        }
    }
</script>

<style>
</style>