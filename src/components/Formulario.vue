<script setup>
    const props = defineProps(['eventoPesquisa', 'valorInput', 'resetInput'])
</script>

<template>
    <form class="pesquisa" @submit.prevent="props.eventoPesquisa" id="form">
        <input class="pesquisa_input" type="text" id="cidade-input" @change="props.valorInput" :value="props.resetInput" placeholder="Digite aqui o local">
        <button class="pesquisa_button" type="submit"><i class="fa-solid fa-magnifying-glass"></i></button>
    </form>
</template>