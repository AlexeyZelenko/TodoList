<template>

<div>
    <div class="card" style="width: 90%; padding: 1% 5%;margin: auto; background: rgba(15, 17, 156, 0.5);">
        <h1 class="card-title">
            <span style="color: #d0ffe5">Задачи</span>
        </h1>
        <h6 class="card-subtitle mb-2 text-muted">
            <span  style="color: white">
              "Мечты сбываются. Просто замени слова: "мечта" на "цель".
            "желание" на "задача", "стремление" на "действие"."
            </span>
            </h6>
        <div>
            <button type="button"
                    class="btn btn-primary"
                    data-toggle="modal"
                    data-target="#exampleModal1" >
                Успех
                <span class="badge badge-success">
                    {{todos.filter(todo => {return todo.done === true}).length}}
                </span>
            </button>

            <button type="button"
                    class="btn btn-primary"
                    data-toggle="modal"
                    data-target="#exampleModal2"
                    style="margin: 5px">
                Ожидают
                <span class="badge badge-warning">
                    {{todos.filter(todo => {return todo.done === false}).length}}
                </span>
            </button>

            <button type="button"
                    class="btn btn-primary"
                    style="margin: 5px">
                Все <span class="badge badge-warning">{{todos.length}}</span>
            </button>

            <button @click="$emit('enlarge-text')"
                    class="btn btn-secondary btn-sm"
                    style="margin-left: 2px"
            >
                Увеличить размер текста
            </button>
            <button @click="$emit('enmin-text')"
                    class="btn btn-secondary btn-sm"
                    style="margin-left: 2px"
            >
                Уменьшить размер текста
            </button>
        </div>

        <div class="modal fade" id="exampleModal1"
             tabindex="-1" role="dialog"
             aria-labelledby="exampleModal1Label"
             aria-hidden="true">
            <div class="modal-dialog"
                 role="document">
                <div class="modal-content">
                    <div class="modal-header"
                         style="background: aqua">
                        <h5 class="modal-title"
                            id="exampleModalLabel1">
                            Выполненные задачи
                        </h5>
                    </div>
                    <div class="modal-body">
                        <div v-for="todo in todos"  :key="todo.id">
                            <div  v-show="!isEditing2 && todo.done">
                                <div>
                                    <img src="https://iconizer.net/files/Human_o2/orig/package-installed-updated.png"
                                         alt=""
                                         style="width: 1rem"/>
                                    {{ todo.title }}
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button"
                                class="btn btn-secondary"
                                data-dismiss="modal">
                            Закрыть
                        </button>
                    </div>
                </div>
            </div>
        </div>


        <div class="modal fade"
             id="exampleModal2"
             tabindex="-1"
             role="dialog"
             aria-labelledby="exampleModalLabel2"
             aria-hidden="true">
            <div class="modal-dialog"
                 role="document">
                <div class="modal-content">
                    <div class="modal-header"
                         style="background: cornflowerblue">
                        <h5 class="modal-title"
                            id="exampleModalLabel2"
                        >Незавершенные задачи
                        </h5>
                    </div>
                    <div class="modal-body">
                        <div v-for="todo in todos"
                             :key="todo.id">
                            <div  v-show="!isEditing3 && !todo.done">
                                <div>
                                    <img src="https://makrus.ru/files/images/faq/1s-udalenie.png"
                                         alt=""
                                         style="width: 1rem"/>
                                    {{ todo.title }}
                                </div>
                            </div>
                        </div>
                    </div>
                    <div class="modal-footer">
                        <button type="button"
                                class="btn btn-secondary"
                                data-dismiss="modal">
                            Закрыть
                        </button>
                    </div>
                </div>
            </div>
        </div>

        <div>
            <todo
                    v-on:delete-todo="deleteTodo"
                    v-on:complete-todo="completeTodo"

                    v-for="todo in todos"
                    :todo.sync="todo"
                    :key="todo.id">
            </todo>
        </div>
    </div>


    <div class="fluid container">
        <div class="form-group form-group-lg panel panel-default">
            <div class="panel-heading">
                <h3 class="panel-title" style="color: #9de0f6">Расставь свои приоритеты</h3>
            </div>
            <div class="panel-body">
                <div class="checkbox">
                    <label style="color: #9de0f6"><input type="checkbox" v-model="editable">Сортировать\не сортировать</label>
                </div>
                <button type="button" class="btn btn-dark" @click="orderList" style="color: #9de0f6">Сортировать в оригинальном порядке</button>
            </div>
        </div>

        <div class="col-md-3" style="max-width: 40% ">
            <draggable class="list-group" tag="ul" v-model="list" v-bind="dragOptions" :move="onMove" @start="isDragging=true" @end="isDragging=false">
                <transition-group type="transition" :name="'flip-list'">
                    <li class="list-group-item" v-for="element in list" :key="element.order">
                        <i :class="element.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'" @click=" element.fixed=! element.fixed" aria-hidden="true"></i>
                        {{element.name}}
                        <span class="badge">{{element.order}}</span>
                    </li>
                </transition-group>
            </draggable>
        </div>

        <div class="col-md-3" style="background: #9de0f6; max-width: 40%">
            <draggable element="span" v-model="list2" v-bind="dragOptions" :move="onMove">
                <transition-group name="no" class="list-group" tag="ul">
                    <li class="list-group-item" v-for="element in list2" :key="element.order">
                        <i :class="element.fixed? 'fa fa-anchor' : 'glyphicon glyphicon-pushpin'" @click=" element.fixed=! element.fixed" aria-hidden="true"></i>
                        {{element.name}}
                        <span class="badge">{{element.order}}</span>
                    </li>
                </transition-group>
            </draggable>
        </div>


        <div class="list-group col-md-3">
            <pre style="color: #9de0f6">{{listString}}</pre>
        </div>
        <!--<div class="list-group col-md-3" >-->
            <!--<pre style="color: #f968a5">{{list2String}}</pre>-->
        <!--</div>-->
    </div>


</div>

</template>

<script>

    import Todo from './Todo';
    import Swal from 'sweetalert2';
    import draggable from 'vuedraggable';


    let message =
        [
            "Бог",
            'Семья',
            "Работа",
            "Отдых",
            "Хобби",

        ];


    export default {
        name: "hello",
        props: ['todos'],

        components: {
            Todo,
            draggable,

        },

        data() {
            return {
                list: message.map((name, index) => {
                    return { name, order: index + 1, fixed: false };
                }),
                list2: [],
                editable: true,
                isDragging: false,
                delayedDragging: false,


                isEditing: false,
                isEditing2: false,
                isEditing3: false,


            };
        },
        methods: {
            orderList() {
                this.list = this.list.sort((one, two) => {
                    return one.order - two.order;
                });
            },
            onMove({ relatedContext, draggedContext }) {
                const relatedElement = relatedContext.element;
                const draggedElement = draggedContext.element;
                return (
                    (!relatedElement || !relatedElement.fixed) && !draggedElement.fixed
                );
            },

            showForm() {
                this.isEditing = true;

            },
            hideForm() {
                this.isEditing = false;
            },
            deleteTodo(todo) {
                Swal.fire({
                    title: 'Вы уверенны?',
                    text: "Вы не сможете вернуть это!",
                    type: 'warning',
                    showCancelButton: true,
                    confirmButtonColor: '#3085d6',
                    cancelButtonColor: '#d33',
                    confirmButtonText: 'Да, удалить это!'
                }).then((result) => {
                        const todoIndex = this.todos.indexOf(todo);
                        this.todos.splice(todoIndex, 1);
                    if (result.value) {
                        Swal.fire(
                            'Удаленно!',
                            'Ваш файл был удален.',
                            'success'
                        );
                    }
                });
            },
            completeTodo(todo) {
                Swal.fire({
                    title: 'Поздравляю!',
                    width: 300,
                    padding: '4em',
                    background: '#fff url(/images/trees.png)',
                    backdrop: `
    rgba(0,0,123,0.4)
    url("https://cdn.pixabay.com/photo/2013/07/13/09/35/darts-155726_960_720.png")
    center left
    no-repeat
  `
                })
                const todoIndex = this.todos.indexOf(todo);
                this.todos[todoIndex].done = true;
            },

        },
        computed: {

            // list() {
            //     return (this.todos.map((todo, index) => {
            //         return {name: todo.title, order: index + 1, fixed: false};
            //
            //     })
            // )},

            dragOptions() {
                return {
                    animation: 0,
                    group: "description",
                    disabled: !this.editable,
                    ghostClass: "ghost"
                };
            },
            listString() {
               let message1 = 'Правильные приоритеты' +
                   ' залог успеха'
                return message1;
            },
            // list2String() {
            //     return JSON.stringify(this.list2, null, 2);
            // }
        },
        watch: {

            isDragging(newValue) {
                if (newValue) {
                    this.delayedDragging = true;
                    return;
                }
                this.$nextTick(() => {
                    this.delayedDragging = false;
                });
            }
        },
    };

</script>

<style scoped>
    .flip-list-move {
        transition: transform 0.5s;
    }
    .no-move {
        transition: transform 0s;
    }
    .ghost {
        opacity: 0.5;
        background: #c8ebfb;
    }
    .list-group {
        min-height: 20px;
    }
    .list-group-item {
        cursor: move;
    }
    .list-group-item i {
        cursor: pointer;
    }
</style>
