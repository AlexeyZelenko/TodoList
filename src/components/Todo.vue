<template>
    <!--редактирование-->
    <div class="card text-center" style="background: rgba(15, 17, 156, 0.5);">
        <div class="alert alert-primary" >
            <div >
                <button class="btn btn-success"
                        v-show="todo.done"
                        style="margin-left: -80%;  box-shadow:  0 0 5px rgba(0,0,0,0.5);">
                    <img src="https://nikolskoe-adm.ru/assets/resources/137/galochka.png"
                         alt="" style="width: 2rem; padding-right: 5px;"/>
                    Успех
                </button>
                <button type="button"
                        class="btn btn-danger"
                        v-show="!todo.done"
                        style="margin-left: -70%;  box-shadow:  0 0 5px rgba(0,0,0,0.5);">
                    <img src="https://iconizer.net/files/Vista_Style_Base_Software/thumb/128/Close_Box_Red.png"
                         alt="" style="width: 2rem; padding-right: 5px;"/>
                    Невыполненно
                </button>
                <button @click="count++"
                        class="btn btn-outline-info"
                        style="position: absolute;
                         margin-left: 5px;
                        box-shadow:  0 0 5px rgba(0,0,0,0.5);">
                    Кол-во попыток — {{ count }}
                </button>



            </div>
            <div>
                <div v-show="!isEditing">
                    <div>
                        <p style="fontSize: 1.5em" class="card-title">{{ todo.title }}</p>
                    </div>
                    <div>
                        <p  class="card-text">{{ todo.project }}</p>

                    </div>
                    <div>
                        <span>
                            <button class="btn btn-primary"
                                    type="button"
                                    data-toggle="collapse"
                                    data-target="#collapseExample"
                                    aria-expanded="false"
                                    aria-controls="collapseExample"

                            >
                                Комментарии
                            </button>
                        </span>
                        <div class="collapse" id="collapseExample" >
                            <div >
                                <p style="color: cornflowerblue" >{{todo.comment}}</p>
                            </div>
                        </div>
                    </div>


                        <span  v-on:click="showForm">
                          <button type="button"
                                  class="btn btn-primary">
                              Редактировать
                          </button>
                        </span>

                    <button type="button"
                            class="btn btn-info"
                            @click="deleteTodo(todo)"
                            style="margin: 5px;  box-shadow:  0 0 5px rgba(0,0,0,0.5);">
                        Удалить
                    </button>

                    <button type="button"
                            class="btn btn-warning"
                            @click="completeTodo(todo)"
                            v-show="!isEditing && !todo.done"
                            style="margin: 5px;  box-shadow:  0 0 5px rgba(0,0,0,0.5);">
                        Отметить выполненным
                    </button>

                </div>

                <!--форма видна, когда мы находимся в режиме редактирования-->
                <div v-show="isEditing">
                    <form class="showForm">
                        <div class="form-group">
                            <label for="1"></label>
                            <input type="text"
                                   v-model="todo.title"
                                   class="form-control"
                                   id="todo.id"
                                   placeholder="Описание проэкта">

                            <label for="1"></label>
                            <input type="text"
                                   v-model="todo.comment"
                                   class="form-control"
                                   id="todo.id"
                                   placeholder="Комментарий проэкта">

                            <label for="1"></label>
                            <input type="text"
                                   v-model="todo.project"
                                   class="form-control"
                                   id="todo.id"
                                   placeholder="Проэкт">
                        </div>
                        <div>
                            <button type="button"
                                    class="btn btn-dark"
                                    v-on:click="hideForm">
                                Сохранить
                            </button>
                        </div>

                    </form>

                </div>
            </div>

        </div>

    </div>

</template>

<script type="text/javascript">


    export default {

        props: ['todo'],
        data() {
            return {

                count: 0,

                isEditing: false,
                isEditing2: false,
                isEditing3: false,


            };
        },

        methods: {
            showForm() {
                this.isEditing = true;

            },
            hideForm() {
                this.isEditing = false;
            },
            deleteTodo(todo) {
                this.$emit('delete-todo', todo);
            },
            completeTodo(todo) {
                this.$emit('complete-todo', todo);
            },
        },
    };
</script>

