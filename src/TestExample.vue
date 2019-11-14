<template>
    <div class="example">
        <!--{{ msg }}-->
        <!--'<button @click="count++">Счётчик кликов — {{ count }}</button>'-->
    </div>
</template>

<script>
    export default {

        props: ['count'],

        data() {
            return {
                msg: 'Hello world!',

            }
        }
    }
</script>

<style scoped>
    .example {
        color: red;
    }
</style>
