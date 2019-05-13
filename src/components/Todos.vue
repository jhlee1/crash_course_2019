<template>
    <div>
        <div v-bind:key="todo.id" v-for="todo in todos"> <!-- for each loop 생성. unique한 key가 필요하기 때문에 v-bind:key로 넣어줌  -->
            <TodoItem v-bind:todo="todo" v-on:del-todo="$emit('del-todo', todo.id)" />
        </div>
    </div>
</template>

<script>
import TodoItem from './TodoItem'

export default {
    name: "Todos", // 외부에서 Todos라는 이름으로 이 component를 사용할 수 있게 해줌
    components: {
        TodoItem
    },
    props: ["todos"] // App.vue에서 v-bind로 넘겨준 todos를 받아서 사용할 수 있게 해줌
}
</script>

<style scoped>

</style>

