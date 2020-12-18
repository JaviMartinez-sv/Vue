<template>

<div>
    <div @click="markAsDone">
     <div v-if="!item.completed">{{ item.name }}</div>
     <div class="done" v-if="item.completed">{{ item.name }}</div>
     <button @click="remove()">Eliminar</button>
     </div>
</div>
</template>
<script>
export default {
    name: 'TodoItem',
    props: ['item'],
    methods:{
        markAsDone(){
            debugger
            this.item.completed = !this.item.completed
        },
        remove(){
            console.log(`remove on todoitem`)
            this.$emit('deleted', this.item.id)
        }

    }
}
</script>

<style>
.done {
  text-decoration: line-through;
}
</style>