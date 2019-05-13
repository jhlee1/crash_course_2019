<template>
    <div>
        <form @submit="addTodo"> <!-- 여기서 instance를 생성하고 App.vue에게 넘길 것이므로 지금 당장 emit하지 않고 addTodo를 부름 -->
            <input type="text" v-model="title" name="title" placeholder="Add todo!">
            <input type="submit" value="Submit" class="btn">
        </form>
    </div>
</template>

<script>
import uuid from 'uuid';
export default {
    name: "AddTodo",
    data() {
        return {
            title: ''
        }
    },
    methods: {
        addTodo(e) {
            e.preventDefault();
            const newTodo = {
                // id: uuid.v4(), 서버에서 주어지므로 axios 이용해서 HTTP 연결할 때 삭제
                title: this.title,
                completed: false
            }

            //Send up to parent
            this.$emit('add-todo', newTodo);
            this.title = '';
        }

    }

}
</script>

<style scoped>
    form {
        display: flex;
    }

    input[type="text"] {
        flex: 10;
        padding: 5px;
    }

    input[type="submit"] {
        flex: 2;
    }
</style>

