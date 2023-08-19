<script setup>
    const props = defineProps(['possivelErro', 'evento', 'valorBotao', 'condicaoStatus'])
</script>

<template>
    <div class="sugestao_pais" v-if="props.condicaoStatus" v-show="props.possivelErro">
        <div class="sugestao_pais_container">
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">Paris</button>
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">Tokyo</button>
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">Kyoto</button>
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">Bogota</button>
        </div>
        
        <div class="sugestao_pais_container">
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">Milão</button>
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">Brasilia</button>
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">São Paulo</button>
            <button v-on:click="props.valorBotao" @click="props.evento" class="sugestao_pais_container_button" type="button">Rio de janeiro</button>
        </div>
    </div>
</template>