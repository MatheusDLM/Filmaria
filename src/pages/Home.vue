<template>
    <div id="home">

        <div class="lista-filmes" v-if="loading">
            <Loading/>
        </div>

        <div class="lista-filmes" v-else>
            <article class="filme" v-for="filme in filmes" :key="filme.id">
                <strong class="top-filme">{{filme.nome}}</strong>
                <img :src="filme.foto" :alt="filme.nome">
                <router-link :to="`/filme/${filme.id}`">Acessar</router-link>
            </article>
        </div>

    </div>
  
</template>

<script>
import api from '../service/api';
import Loading from '../components/Loading';


export default {
    components: {
        Loading
    },
    data(){
       return {
        filmes: [],
        loading: true,
        }
    },
    async created(){
        //url https://sujeitoprogramador.com/r-api/?api=filmes
        const response = await api.get('?api=filmes')
        this.filmes = response.data;
        this.loading = false;
    }

}
</script>

<style scoped>
      #home{
        display: flex;
        flex-direction: column;
        align-items: center;
        justify-content: center;
        width: 800px;
    }

    .lista-filmes article{
        display: flex;
        flex-direction: column;
        justify-content: center;
        align-items: center;
        background-color: #FFF;
        margin: 5px;
        padding: 15px; 
        border-radius: 5px;
    }

    .lista-filmes strong{
        padding-bottom: 15px;
        font-size: 20px;
    }

    img{
      max-height: 450px;
      width: 900px;  
    }

    .lista-filmes article a{
        text-decoration: none;
        color: #FFF;
        font-size: 25px;
        background-color: brown;
        width: 100%;
        height: 40px;
        margin-top: -30px;
        text-align: center;
        border-bottom-left-radius: 5px;
        border-bottom-right-radius: 5px; 
    }

    .top-filme{
      color: #FFF;
      margin-bottom: 0px;
      background: brown;
      padding: 15px;
      border-top-left-radius: 20px;
      border-top-right-radius: 20px;
      width: 96.7%;
      text-align: center;
    }
</style>