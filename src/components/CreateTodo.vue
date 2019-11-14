<template>
    <div>

        <button class="btn btn-success btn-lg" @click="openForm" type="button"  data-toggle="modal" data-target="#exampleModal5" style=" box-shadow:  0 0 5px rgba(0,0,0,0.5);">
            Добавить задачу
        </button>

        <!-- Modal -->
        <div  class="modal fade" id="exampleModal5" tabindex="-1" role="dialog" aria-labelledby="exampleModalLabel" aria-hidden="true">
            <div  class="modal-dialog" role="document">
                <div  class="modal-content">
                    <div class="modal-body" v-show="isCreating">

                            <div  style="background: #c5d0ee">
                                <h5 class="card-title">Добавить новую задачу</h5>
                            </div>
                            <div style="background: red">
                                <h6 class="card-subtitle mb-2 text-muted">
                                    <span style="color: aliceblue; position: center">Все поля обязательны для заполнения!</span>
                                </h6>
                            </div>
                            <div>
                                <h5 class="card-title">
                                    <label style="margin: 5px">Описание задачи</label>
                                    <input v-model="titleText" placeholder="Саморазвитие">
                                </h5>
                            </div>
                            <div>
                                <h6 class="card-title">
                                    <label style="margin: 5px">Проэкт</label>
                                    <input v-model="projectText" type='text' placeholder="Выучить слова">
                                </h6>
                            </div>
                            <div>
                                <h6 class="card-title">
                                    <label style="margin: 5px">Комментарий</label>
                                    <input v-model="commentText" type='text' placeholder="Duolingo">
                                </h6>
                            </div>
                    </div>
                    <div class="modal-footer" style="background: #c5d0ee">
                        <button type="button" class="btn btn-secondary" data-dismiss="modal" @click="closeForm()" style=" box-shadow:  0 0 5px rgba(0,0,0,0.5);">Отмена</button>
                        <button type="button" class="btn btn-outline-success" @click="sendForm()" data-dismiss="modal" style="margin-left: 5px;  box-shadow:  0 0 5px rgba(0,0,0,0.5);">
                            Создать
                        </button>

                    </div>
                </div>
            </div>
        </div>


    </div>
</template>

<script>
    import Swal from 'sweetalert2';

    export default {
        name: 'createTodo',
        data() {
            return {
                titleText: '',
                projectText: '',
                commentText: '',
                isCreating: false,
                idNumber: '',
            };
        },
        methods: {
            openForm() {
                this.isCreating = true;
            },
            closeForm() {
                this.isCreating = false;
            },
            sendForm() {
                Swal.fire({
                    position: 'top',
                    icon: 'success',
                    title: 'Задача добавлена!',
                    showConfirmButton: false,
                    timer: 1500
                });
                if (this.titleText.length > 0 && this.projectText.length > 0) {
                    const title = this.titleText;
                    const project = this.projectText;
                    const comment = this.commentText;
                    this.$emit('create-todo', {
                        title,
                        project,
                        comment,
                        done: false,
                    });
                    this.titleText = '';
                    this.projectText = '';
                    this.idNumber = '';
                    this.comment = '';
                    this.isCreating = false;

                }
            },
        },
    };
</script>
