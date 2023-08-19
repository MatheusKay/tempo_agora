<script setup>
    const props = defineProps(['possivelErro', 'condicaoVisivel', 'loopInfo', 'nome', 'temp', 'condicaoTemp', 'humidade', 'focaDoVento', 'imgStatus'])
</script>

<template>
    <div class="info_localizaca_container" v-if="props.condicaoVisivel" v-show="props.possivelErro">
        <div class="info_localizacao">
            <p class="cidade_name">
            <i class="fa-solid fa-location-dot"></i> {{ props.nome }} 
            </p>
        </div>
        <p class="temp_atual">
            {{ props.temp }} &deg;C
        </p>
        <div class="info_status">
            <p class="info_status_desc">
            {{ props.condicaoTemp }} 
            </p>
            <img :src="props.imgStatus" alt="Imagem que representa o tempo atual">
        </div>
        <div class="detalhes_temp">
            <p>
            <i class="fa-solid fa-droplet"></i>  {{ props.humidade }}%
            </p>
            |
            <p>
            <i class="fa-solid fa-wind"></i> {{ props.focaDoVento }} km/h
            </p>
        </div>
    </div>
</template>