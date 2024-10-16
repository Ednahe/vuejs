<template>
  <div>
    <h1 :id="`h1-${count}`" :style="{color: count > 5 ? 'red' : 'green'}" :class="{active: count > 5}">compteur : {{ count }}</h1>
    <div v-if="count >= 5">Bravo vous avez cliqué plus de 5 fois.</div>
    <div v-else>Vous avez cliqué moins de 5 fois</div>
    <button @click='increment'>Incrémenter</button>
    <button @click="decrement">Décrémenter</button>
    <hr>
    <button @click="sortMovie">Réorganiser</button>
    <form action="" @submit.prevent="addMovie">
      <input type="text" placeholder="Nouveau film" v-model="movieName">
      <button>Ajouter le film</button>
    </form>
    <ul>
      <li v-for="movie in movies" :key="movie">
        {{ movie }} <button @click="deleteMovie(movie)">Supprimer</button>
      </li>
    </ul>
    <hr>
    <ul>
      <li>{{ person.firstName }}</li>
      <li>{{ person.lastName }}</li>
      <li>{{ person.age }}</li>
    </ul>
    <button @click.prevent="randomAge">Changer l'âge</button>
  </div>
</template>

<script setup>
  import { ref } from 'vue';

  const count = ref(0)
  const movieName = ref('')
  const movies = ref([
    'Matrix', 'Anatole', 'Babar'
  ])
  const person = ref({
    firstName : 'john',
    lastName : 'doe',
    age : 32,
  })

  console.log(count, count.value);
  
  const increment = () => {
    count.value++;
  }
  const decrement = () => {
    count.value--;
  }

  const deleteMovie = (movie) => {
    movies.value = movies.value.filter(m => m !== movie);
  }

  const sortMovie = () => {
    movies.value.sort((a,b) => a > b ? 1 : -1);
  }

  const addMovie = () => {
    movies.value.push(movieName.value);
    movieName.value = '';
  }

  const randomAge = () => {
      person.value = {
        ...person.value,
        age:  Math.round(Math.random() * 100)
      }
    }
</script>

<style>
.active {
  border: 2px double orange;
}
</style>