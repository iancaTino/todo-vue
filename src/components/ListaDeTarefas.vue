<script setup>
const props = defineProps(['tarefas'])
const emit = defineEmits(['toggle'])
</script>

<template>
    <ul class="list-group mt-4">
        <li class="list-group-item" v-for="(tarefa, index) in props.tarefas" :key="index">
            <input type="checkbox" :checked="tarefa.finalizada"
                @change="e => emit('toggle', { index, checked: e.target.checked })">

            <label class="ms-3" :class="{ done: tarefa.finalizada }">
                {{ tarefa.titulo }}
            </label>
        </li>
    </ul>
</template>

<style scoped>
.done {
    text-decoration: line-through;
}
</style>