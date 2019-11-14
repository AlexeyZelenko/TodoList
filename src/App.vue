<template >
    <div style="
    background-image: url(https://i.ytimg.com/vi/Ws7nTP-JOiY/maxresdefault.jpg);
    background-repeat: repeat;
    background-size: auto;
">
        <div style="
        position: fixed;
        right: -10%;
        top: 1%;
        width:347px;
        height:160px;
        display: block;
        z-index:99999999;
">
            <create-todo @create-todo="createTodo"></create-todo>
        </div>
        <div>
            <todo-list :todos="todos"
                       :style="{ fontSize: postFontSize + 'em' }"
                       v-on:enlarge-text="postFontSize += 0.1"
                       v-on:enmin-text="postFontSize -= 0.1"
            ></todo-list>
        </div>

        <div>
            <TestExample :count='cou'></TestExample>
        </div>
        <div>
            <CommentsTodo :people="people" @message="displayMessage"></CommentsTodo>
        </div>




    </div>
</template>
<script>

    import TodoList from './components/TodoList';
    import CreateTodo from './components/CreateTodo';
    import TestExample from './TestExample.vue';
    import CommentsTodo from './components/CommentsTodo';


    export default {
        name: 'app',

        components: {
            TodoList,
            CreateTodo,
            TestExample,
            CommentsTodo,
        },
        //функция данных предоставляет данные в шаблон
        data() {
            return {
                postFontSize: 1,
                cou: 0,

                todos: [{
                    id: 1,
                    title: 'Купить апельсины',
                    project: 'Приоритет A',
                    comment: 'Сочные',
                    done: false,
                }, {
                    id: 2,
                    title: 'Отремонтировать машину',
                    comment: 'Смотреть список',
                    project: 'Приоритет B',
                    done: true,
                }, {
                    id: 3,
                    title: 'Поспать',
                    project: 'Приоритет C',
                    comment: '',
                    done: true,
                }],
                people: [
                    {
                        title: 'Max',
                        id: 1,
                    },
                    {
                        title: 'Jack',
                        id: 2,
                    },
                    {
                        title: 'Leo',
                        id: 3,
                    }],



            }
        },
        methods: {
            createTodo(newTodo) {
                this.todos.push(newTodo);
            },
            displayMessage(message) {
                this.people.push(message);
            },
        }
    }

</script>
