<script setup lang="ts">
import { reactive } from 'vue';

import { Gender, Popularity, Length, names } from '@/data';
import { CardName } from '#components';

interface OptionsState {
  gender: Gender,
  popularity: Popularity,
  length: Length,
}

const options = reactive<OptionsState>({
  gender: Gender.GIRL,
  popularity: Popularity.UNIQUE,
  length: Length.LONG,
});

const selectedNames = ref<string[]>([]);

const removeName = (index : number) => {
  const filteredNames = [...selectedNames.value];
  filteredNames.splice(index, 1)
  selectedNames.value = filteredNames;
}

const optionsArray = [
  {
    title: "1. Choose a gender",
    category: "gender",
    buttons: [Gender.GIRL, Gender.BOY, Gender.UNISEX],
  },
  {
    title: "2. Choose the name's popularity",
    category: "popularity",
    buttons: [Popularity.TRENDY, Popularity.UNIQUE],
  },
  {
    title: "3. Choose the name's length",
    category: "length",
    buttons: [Length.LONG, Length.ALL, Length.SHORT],
  },
]

const computeSelectedNames = () => {
  const filteredNames = names
    .filter((name) => name.gender === options.gender)
    .filter((name) => name.popularity === options.popularity)
    .filter((name) => {
      if (options.length === Length.ALL) return true;
      else return name.length === options.length;
    });
  selectedNames.value = filteredNames.map((name) => {
    return name.name;
  });
};

</script>

<template>
  <div class="container">
    <h1>Name Generator</h1>
    <p>Choose your options and click the "Find Names Button" below </p>
    <div class="options-container">
      <Option v-for="option in optionsArray" :key="option.title" :option="option" :options="options" />
      <button class="primary" @click="computeSelectedNames">Find Names</button>
    </div>
    <div class="cards-container">
      <CardName v-for="(name, index) in selectedNames" :key="name" :name="name" @remove="()=> removeName(index)" :index="index" />
    </div>
  </div>
</template>

<style scoped>
.container {
  font-family: Arial, Helvetica, sans-serif;
  color: rgb(27, 60, 138);
  max-width: 50rem;
  margin: 0 auto;
  text-align: center;
}

.container h1 {
  font-size: 3rem;
}

.options-container {
  background-color: rgb(255, 238, 236);
  border-radius: 2rem;
  padding: 1rem;
  width: 90%;
  margin: 0 auto;
  margin-top: 2rem;
  position: relative;
}

.option-container {
  margin-bottom: 2rem;
}

.option {
  background-color: white;
  outline: 0.15rem solid rgb(249, 87, 89);
  border: none;
  padding: 0.75rem;
  width: 12rem;
  font-size: 1rem;
  color: rgb(27, 60, 138);
  cursor: pointer;
  font-weight: 200;
}

.option-left {
  border-radius: 1rem 0 0 1rem;
}

.option-right {
  border-radius: 0 1rem 1rem 0;
}

.option-active {
  background-color: rgb(249, 87, 89);
  color: white;
}

.primary {
  background-color: rgb(249, 87, 89);
  color: white;
  border-radius: 6.5rem;
  padding: 0.75rem 4rem;
  border: none;
  font-size: 1rem;
  margin-top: 1rem;
  cursor: pointer;
}

.cards-container {
  display: flex;
  flex-wrap: wrap;
  margin-top: 3rem;
  align-items: center;
  justify-content: center;
}


</style>
