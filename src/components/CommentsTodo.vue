<template>
    <div class="white">
        <input type="text" v-model="message" @keyup.enter="saveMessage">
       <h2 >Участники</h2>
        <ul>
            <li v-for="person in people" :key="person.id">
                {{person.title}}
            </li>
        </ul>
    </div>
</template>

<script>
    export default {
        name: 'CommentsTodo',
        props: {
            people: {
                type: Array,
            }
        },
        data() {
            return {
                message: '',
            }
        },
        methods: {
            saveMessage() {
               // alert(this.message)
               this.$emit('message', this.message);
                this.message = ''
            }
        }

    }

</script>

<style scoped>
    .white {
        color: white;
    }
</style>
