<template>
  <h1>Your Super Heroes</h1>
  <form @submit.prevent="addNewHero">
    <label>Name</label>
    <input v-model="newName" name="name" type="text">
    <label>First Name</label>
    <input v-model="newFirstName" name="firstName" type="text">
    <label>Last Name</label>
    <input v-model="newLastName" name="lastName" type="text">
    <label>Place</label>
    <input v-model="newPlace" name="place" type="text">
    <label>Image URL</label>
    <input v-model="newImage" name="imageUrl" type="text">
    <button>Add Super Hero</button>
  </form>
</template>

<script>
import { ref } from 'vue';

export default {
  setup() {
    const newName = ref('');
    const newFirstName = ref('');
    const newLastName = ref('');
    const newPlace = ref('');
    const newImage = ref('');
    const id = Math.floor(Math.random() * 10000) + 1;

    async function addNewHero() {
      const newHero = {
        Id : id,
        Name : newName.value,
        FirstName : newFirstName.value,
        LastName : newLastName.value,
        Place : newPlace.value,
        ImageURL : newImage.value,
      }

      const response = await fetch(`/api/SuperHero`, {
        method: 'POST',
        headers: {'Content-Type': 'application/json'},
        body: JSON.stringify(newHero)
      })
      return await response.json();
    }

    return {
      newName,
      newFirstName,
      newLastName,
      newPlace,
      newImage,
      addNewHero,
    };
  }
}
</script>

<style>
body {
  font-family: sans-serif;
  padding-top: 1em;
  padding-bottom: 1em;
  font-size: 2em;
  width: 80%;
  margin: 0 auto;
}
input, textarea, button, p, div, section, article, select {
  display: 'block';
  width: 100%;
  font-family: sans-serif;
  font-size: 1em;
  margin: 0.5em;
}
</style>
