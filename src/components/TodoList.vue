<template>
    <div>
        <ol class="todoList">
            <ul v-for="(todoItem, index) in list" :key="index">
                <input type="checkbox" :checked="todoItem.status === 'done'" @change="changeStatus(todoItem, $event)">
                {{ todoItem.name }}
            </ul>
        </ol>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
import Todo from '../models/Todo';
@Component({
    props: {
        list: Array
    }
})
export default class TodoList extends Vue {
    changeStatus(item: Todo, e: Event){
        let status = (<HTMLInputElement>e.target).checked
        this.$emit('updateStatus', item, { status: status ? 'done' : 'todo'} )
    }
}
</script>

<style lang="scss" scoped>

</style>