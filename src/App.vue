<template>
    <section class="todoapp">
        <TodoHeader @add="addFn"></TodoHeader>
        <TodoMain
            :list="shownList"
            @listDone="listDoneFn"
            @del="delFn"
            @selectAll="selectAllFn"
        ></TodoMain>
        <TodoFooter
            :list="list"
            @clearCompleted="clearCompletedFn"
            v-show="list.length > 0"
            @changeList="changeListFn"
        ></TodoFooter>
    </section>
</template>

<script>
import TodoHeader from './components/TodoHeader.vue'
import TodoMain from './components/TodoMain.vue'
import TodoFooter from './components/TodoFooter.vue'
export default {
    components: {
        TodoHeader,
        TodoMain,
        TodoFooter,
    },
    data() {
        return {
            list: JSON.parse(localStorage.getItem('todoList')) || [],
            type: 'all',
        }
    },
    methods: {
        listDoneFn(id) {
            const p = this.list.find(item => item.id === id)
            p.ifDone = !p.ifDone
        },
        delFn(id) {
            this.list = this.list.filter(item => item.id !== id)
        },
        addFn(info) {
            this.list.unshift({
                id: +new Date(),
                title: info,
                ifDone: false,
            })
        },
        clearCompletedFn() {
            this.list = this.list.filter(item => item.ifDone === false)
        },
        changeListFn(type) {
            this.type = type
        },
        selectAllFn(value) {
            this.list.forEach(item => item.ifDone = value)
        },
    },
    computed: {
        shownList() {
            if (this.type === 'all') {
                return this.list
            } else if (this.type === 'active') {
                return this.list.filter(item => item.ifDone === false)
            } else {
                return this.list.filter(item => item.ifDone === true)
            }
        },
    },
    watch: {
        list: {
            deep: true,
            handler() {
                localStorage.setItem('todoList', JSON.stringify(this.list))
            },
        },
    },
}
</script>

<style></style>
