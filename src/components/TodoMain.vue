<template>
    <!-- This section should be hidden by default and shown when there are todos -->
    <section class="main">
        <input
            id="toggle-all"
            class="toggle-all"
            type="checkbox"
            v-model="isAll"
        />
        <label for="toggle-all">Mark all as complete</label>
        <ul class="todo-list">
            <!-- These are here just to show the structure of the list items -->
            <!-- List items should get the class `editing` when editing and `completed` when marked as completed -->
            <li
                :class="{ completed: item.ifDone }"
                v-for="item in list"
                :key="item.id"
            >
                <div class="view">
                    <input
                        class="toggle"
                        type="checkbox"
                        :checked="item.ifDone"
                        @change="ifDoneFn(item.id)"
                    />
                    <label>{{ item.title }}</label>
                    <button class="destroy" @click="del(item.id)"></button>
                </div>
                <input class="edit" value="Create a TodoMVC template" />
            </li>
        </ul>
    </section>
</template>

<script>
export default {
    props: {
        list: { type: Array, required: true },
    },
    methods: {
        ifDoneFn(id) {
            this.$emit('listDone', id)
        },
        del(id) {
            this.$emit('del', id)
        },
    },
    computed: {
        isAll: {
            get() {
                return this.list.every(item => item.ifDone === true)
            },
            set(value) {
                console.log(value)
                this.$emit('selectAll', value)
            },
        },
    },
}
</script>

<style></style>
