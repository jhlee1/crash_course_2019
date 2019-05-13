<template>
    <div class="todo-item" v-bind:class="{'is-completed': todo.completed}"> <!-- {value:condition} 만약 condition이 true면 value값이 들어간다 -->
        <p>
            <input type="checkbox" v-on:change="markComplete"> <!-- 체크박스가 체크 / 언체크 되는 타이밍에 이벤트를 발생시키면서 markComplete 함수를 부름-->
            {{todo.title}}
            <button @click="$emit('del-todo', todo.id)" class="del">x</button> <!-- 실제 data를 가지고 있는게 App.vue이기 때문에 이 정보를 위로 올려줘서 App.vue에서 처리해야함. 여기선 todo.id를 payload로 올려줌 -->
        </p>
    </div>
</template>

<script>
export default {
    name: "TodoItem",
    props: ["todo"],
    methods: {
        markComplete() {
            this.todo.completed = !this.todo.completed; //checked 될 때 마다 completed를 반댓값으로 바꿈(true-> false, false -> true)
        }
    }
}
</script>

<style scoped>
.todo-item {
    background: #f4f4f4;
    padding: 10px;
    border-bottom: 1px #ccc dotted;
}

.is-completed {
    text-decoration: line-through;
}

.del {
    background: #ff0000;
    color:#fff;
    border: none;
    padding: 5px 9px;
    border-radius: 50%;
    cursor: pointer;
    float: right;
}
</style>

