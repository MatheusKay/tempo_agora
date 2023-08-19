<script setup>
  import { reactive } from 'vue';
  import Formulario from './components/Formulario.vue';
  import Sugestao from './components/Sugestao.vue';
  import InfoCidade from './components/InfoCidade.vue';

  const apiKey = "37d86dee361841d08c6233406231808";
  const apiUnsplash = "https://source.unsplash.com/1600x900/?";

  const estado = reactive({

    cidade: '',
    nomeLugar: '',
    tempLugar: '',
    condicaoLugar: '',
    humidadeLugar: '',
    forcaVentoLugar: '',
    imgStatus: '',
    botaoStatus: '',
    erroNaBusca: true,

  })

  //Funções

  const getWeatherData = async (city) => {
  
    const apiWeatherURL = `https://api.weatherapi.com/v1/current.json?key=${apiKey}&q=${city}&lang=pt`

    try {

      const res = await fetch(apiWeatherURL)
      const data = await res.json();

      return data;

    } catch (error) {
      
      console.error('Ocorreu um erro ao obter os dados do clima:', error)
      throw error;

    }

  }

  const showWeatherData = async () => {

    estado.erroNaBusca = true
    let data;

    try {

      if(estado.cidade !== '') {
        data = await getWeatherData(estado.cidade);
      } else {
        data = await getWeatherData(estado.botaoStatus)
      }

      estado.nomeLugar = data.location.name
      estado.tempLugar = parseInt(data.current.temp_c)
      estado.condicaoLugar = data.current.condition.text
      estado.imgStatus = 'https:' + data.current.condition.icon
      estado.humidadeLugar = data.current.humidity
      estado.forcaVentoLugar = data.current.wind_kph

      document.body.style.backgroundImage = `url("${apiUnsplash + data.location.country}")`
    
      estado.cidade = '';

    } catch(error) {

      if(data.error.code === 1006) {
        estado.cidade = '';
        estado.erroNaBusca = false
      }

    }

  }
</script>

<template>
  
  <div class="container">
    <h3 class="titulo_text">Confira o clima de uma cidade:</h3>
    <Formulario :evento-pesquisa="showWeatherData" :valor-input="evento => estado.cidade = evento.target.value" :reset-input="estado.cidade"></Formulario>
    <Sugestao :valor-botao="evento => estado.botaoStatus = evento.target.textContent" :evento="showWeatherData" :condicao-status="estado.nomeLugar == ''" :possivel-erro="estado.erroNaBusca"></Sugestao>
    <InfoCidade :condicao-visivel="estado.nomeLugar !== ''" :nome="estado.nomeLugar" :temp="estado.tempLugar" :condicao-temp="estado.condicaoLugar" :humidade="estado.humidadeLugar" :foca-do-vento="estado.forcaVentoLugar" :img-status="estado.imgStatus" :possivel-erro="estado.erroNaBusca == true"></InfoCidade>
    
    <div class="mensagem_erro" v-show="!estado.erroNaBusca">
      <p>
        Não foi possivel localizar o lugar que você pesquisou, tente novamente!
      </p>
    </div>
  </div>

</template>

<style scoped>
</style>
