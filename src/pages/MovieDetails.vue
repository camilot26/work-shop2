<template>
     <div class="container">
        <div class="card">
            <h2>{{ movie?.Title }}</h2>
            <div class="card-header">
                <img :src="movie?.Poster" :alt="movie?.Title" />
                
                
            </div>
        
            <div class="team">
                 
    <p>
        <p>
      <span>Plot:</span>
      {{ movie?.Plot }}
    </p>
      <span>Año:</span>
      {{ movie?.Year }}
    </p>
    <p>
      <span>Género:</span>
      {{ movie?.Genre }}
    </p>
    <p>
      <span>Director:</span>
      {{ movie?.Director }}
    </p>
    <p>
      <span>Cast:</span>
      {{ movie?.Actors }}
    </p>
    
    <p>
      <span>Writer:</span>
      {{ movie?.Writer }}
    </p>

    <p>
      <span>Awards:</span>
      {{ movie?.Awards }}
    </p>
    <p>
      <span>Actors:</span>
      {{ movie?.Actors }}
    </p>
    <p>
      <span>Languege:</span>
      {{ movie?.Language }}
    </p>
            </div>
            <div class="tags">
                <button class="btn"><router-link :to="{ name: 'home'}">HOME</router-link> </button>
            </div>
        </div>

        </div>




    
    

  

</template>

<script setup lang="ts">
import { useRoute } from 'vue-router'
import axios from 'axios';
import { defineProps, onMounted,ref } from 'vue';
import router from '../router/movies.router';
const route = useRoute();
const movieId = route.params.id as string;

onMounted(()=> {    
    console.log('aaa')
    getMovieDetails()
    
    
})
    interface IProps {
        Title: string,
        Year: number
        Genre: string,
        Director: string,
        Cast: string,
        Plot: string,
        Writer: string,
        Poster: string,
        Awards: string,
        Actors: string,
        Language: string
      }
      const movie = ref<IProps | null>(null); 
      
      async function getMovieDetails(){
        
        try {
            
            const response = await axios.get(`https://www.omdbapi.com/?i=${movieId}&apikey=21544ac9`);
            movie.value=response.data;
           
            
            
        }catch (error) {
            console.error('Error fetching movie details:', error);

      }
    }
</script>

<style lang="scss" scoped>
    


    .btn{

        min-width: 130px;
  height: 40px;
  color: #fff;
  padding: 5px 10px;
  font-weight: bold;
  cursor: pointer;
  transition: all 0.3s ease;
  position: relative;
  display: inline-block;
  outline: none;
  border-radius: 5px;
  z-index: 0;
  background: #fff;
  overflow: hidden;
  border: 2px solid #212529;
  color: #212529;
       
    }
    .btn:hover{
       
        color: #fff;
    }
    .btn:hover:after {
  height: 100%;
}
.btn:after {
    content: "";
  position: absolute;
  z-index: -1;
  transition: all 0.3s ease;
  left: 0;
  top: 0;
  height: 0;
  width: 100%;
  background: #037bf3;
}



    .container {
   
    margin-top: 20px;
    align-items:center ;
    flex-wrap: wrap;
    padding: 10px;
    
}

.card {
    background-color: #0e0d0d;
    border-radius: 8px;
    box-shadow: 5px 5px 10px rgb(191, 176, 176);
    display: flex;
    align-items: center;
   gap:25px;
   
    padding: 15px;
    box-sizing: border-box;
    h2{
        color: blue;
    }
    h2:hover{
        color: rgb(252, 3, 3);
        
        
    }
}

.card-header {
    display: flex;
    justify-content: center;
    img{
        border-radius: 12px;
        box-shadow: 1px 1px 30px rgb(151, 2, 2);
    }
}
.team {
    display: flex;
    justify-content: center;
    flex-direction: column;
    margin: 10px 0;
    span{
        color:red;
        
    }
    p{
        color:white;
    }
}




</style>
