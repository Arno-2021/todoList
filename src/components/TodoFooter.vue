<template>
    <!-- This footer should be hidden by default and shown when there are todos -->
    <footer class="footer">
        <!-- This should be `0 items left` by default -->
        <span class="todo-count"
            ><strong>{{ countActive }}</strong> item left</span
        >
        <!-- Remove this if you don't implement routing -->
        <ul class="filters">
            <li>
                <a
                    :class="{ selected: type === 'all' }"
                    href="#/"
                    @click.prevent="switchBar('all')"
                    >All</a
                >
            </li>
            <li>
                <a
                    href="#/active"
                    @click.prevent="switchBar('active')"
                    :class="{ selected: type === 'active' }"
                    >Active</a
                >
            </li>
            <li>
                <a
                    href="#/completed"
                    @click.prevent="switchBar('completed')"
                    :class="{ selected: type === 'completed' }"
                    >Completed</a
                >
            </li>
        </ul>
        <!-- Hidden if no completed items are left ↓ -->
        <button class="clear-completed" v-show="ifShow" @click="clearCompleted">
            Clear completed
        </button>
    </footer>
</template>

<script>
export default {
    props: {
        list: {
            type: Array,
        },
    },
    data() {
        return {
            type: 'all',
        }
    },
    computed: {
        countActive() {
            return this.list.filter(item => item.ifDone === false).length
        },
        ifShow() {
            return this.list.some(item => item.ifDone === true)
        },
    },
    methods: {
        clearCompleted() {
            this.$emit('clearCompleted')
        },
        switchBar(type) {
            this.type = type
            this.$emit('changeList', this.type)
        },
    },
}
</script>

<style></style>
