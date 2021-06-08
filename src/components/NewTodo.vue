<template>
    <div class="inputBox">
        <input type="text" v-model="text" ref="input">
        <button @click="addTodo">添加</button>
    </div>
</template>

<script lang="ts">
import { Component, Vue } from 'vue-property-decorator';
@Component
export default class NewTodo extends Vue{
    $refs!: {
        input: HTMLInputElement
    }
    text:String = ''

    mounted() {
        this.$refs.input.focus()
    } 

    addTodo(){
        this.$emit('addTodo', this.text)
        this.text = ''
        this.$refs.input.focus()
    }
}
</script>

<style lang="scss" scoped>

</style>