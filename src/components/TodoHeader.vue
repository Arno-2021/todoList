<template>
    <header class="header">
        <h1>todos</h1>
        <input
            class="new-todo"
            placeholder="What needs to be done?"
            autofocus
            v-model="info"
            @keyup.enter="add"
        />
    </header>
</template>

<script>
export default {
    data() {
        return {
            info: '',
        }
    },
    methods: {
        add() {
            if (this.info.trim() === '') {
                return 
            }
            this.$emit('add', this.info)
            this.info = ''
        },
    },
}
</script>

<style></style>
