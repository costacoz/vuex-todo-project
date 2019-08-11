<template>
    <div>
        <h3>Todos</h3>
        <div class="legend">
            <span>Double click on title to change it</span>
        <span>
            <span class="incomplete-box"></span> = Incomplete
        </span>
        <span>
            <span class="complete-box"></span> = Complete
        </span>
        </div>
        <div class="todos">
            <div
                    v-for="todo in allTodos"
                    :key="todo.id"
                    v-bind:class="{'is-complete':todo.completed}"
                    class="todo"
            >
                <Todo v-bind:todo="todo"/>
                <i class="fas fa-check-square completed" @click="changeCompleteness(todo)"></i>
                <i class="far fa-check-square incompleted" @click="changeCompleteness(todo)"></i>
                <i class="fas fa-trash-alt delete" @click="deleteTodo(todo.id)"></i>
            </div>
        </div>
    </div>
</template>
<script>
    import {mapGetters, mapActions} from 'vuex';
    import Todo from "@/components/Todo";

    export default {
        name: "Todos",
        components: {Todo},
        methods: {
            ...mapActions(['fetchTodos', 'deleteTodo', 'updateTodo']),
            changeCompleteness(todo){
                const updatedTodo = {
                  id: todo.id,
                  title: todo.title,
                  completed: !todo.completed,
                };
                this.updateTodo(updatedTodo);
            },
        },
        computed: mapGetters(['allTodos']),
        created() {
            this.fetchTodos()
        }
    }
</script>
<style scoped>
    .todos {
        display: grid;
        grid-template-columns: repeat(3, 1fr);
        grid-gap: 1rem;
    }

    .todo {
        border: 1px solid #ccc;
        background: #41b883;
        padding: 1rem;
        border-radius: 5px;
        text-align: center;
        position: relative;
        cursor: pointer;
    }

    .delete {
        position: absolute;
        bottom: 10px;
        right: 10px;
        color: #fff;
        cursor: pointer;
    }

    .incompleted, .completed {
        position: absolute;
        bottom: 10px;
        left: 10px;
        color: #fff;
        cursor: pointer;
    }

    .legend {
        display: flex;
        justify-content: space-around;
        margin-bottom: 1rem;
    }

    .complete-box {
        display: inline-block;
        width: 10px;
        height: 10px;
        background: #35495e;
    }

    .incomplete-box {
        display: inline-block;
        width: 10px;
        height: 10px;
        background: #41b883;
    }

    .is-complete {
        background: #35495e;
        color: #fff;
        text-decoration: line-through;
    }

    .is-complete .incompleted {
        display: none;
    }

    .is-complete .completed {
        display: block;
    }

    .completed {
        display: none;
    }

    @media (max-width: 500px) {
        .todos {
            grid-template-columns: 1fr;
        }
    }
</style>