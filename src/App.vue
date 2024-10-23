<template>
  <div class="form-container">
    <h1>Find artikler tæt på dig!</h1>
    <p>Indtast, hvor mange kilometer du ønsker fra det valgte postnummer.</p>

    <form @submit.prevent="submitForm">
      <div class="form-group">
        <input type="number" v-model="distance" placeholder="50" required />
        <label for="distance">km fra</label>
        <input type="number" v-model="postcode" placeholder="8000" required />
      </div>

      <button type="submit" class="submit-button">Vis</button>
    </form>

    <div v-if="items.length > 0" class="items-list">
      <h2>Artikler fundet: {{ items.length }}</h2>
      <!-- Totalt antal artikler -->
      <div class="grid-container">
        <div v-for="(item, index) in items" :key="index" class="grid-item">
          {{ item }}
        </div>
      </div>
    </div>
  </div>
</template>

<script setup>
import { ref } from 'vue';

// Define reactive state variables
const distance = ref(15); // Default value for distance
const postcode = ref(8000); // Default value for postcode
const items = ref([]); // List of items to show

// Function to handle form submission
function submitForm() {
  generateItems();
}

// Function to generate items based on distance
function generateItems() {
  // Clear current items
  items.value = [];

  // Calculate number of items (10 items for each km in distance)
  const numberOfItems = distance.value * 4;

  // Generate items and add them to the items array
  for (let i = 1; i <= numberOfItems; i++) {
    items.value.push(`Artikel ${i}`);
  }
}
</script>

<style scoped>
body {
  font-family: Arial, sans-serif;
  background-color: #4a7c80;
  display: flex;
  justify-content: center;
  align-items: center;
  height: 100vh;
  margin: 0;
}

.form-container {
  text-align: center;
  background-color: #467a7d;
  padding: 30px;
  border-radius: 10px;
  box-shadow: 0 4px 10px rgba(0, 0, 0, 0.1);
}

h1 {
  color: white;
}

p {
  color: white;
}

.form-group {
  display: flex;
  justify-content: center;
  align-items: center;
  margin-bottom: 20px;
}

.form-group input {
  width: 80px;
  padding: 10px;
  margin: 0 5px;
  border: 1px solid #ccc;
  border-radius: 5px;
  font-size: 16px;
  text-align: center;
}

.form-group label {
  color: white;
  font-size: 16px;
  margin: 0 10px;
}

.submit-button {
  background-color: #3e6f72;
  color: white;
  padding: 12px 40px;
  border: none;
  border-radius: 5px;
  cursor: pointer;
  font-size: 18px;
  transition: background-color 0.3s ease;
}

.submit-button:hover {
  background-color: #2f585b;
}

.items-list {
  margin-top: 20px;
}

.items-list h2 {
  color: white;
}

.grid-container {
  display: grid;
  grid-template-columns: repeat(2, 1fr); /* 2 items per row */
  gap: 20px;
  margin-top: 20px;
}

.grid-item {
  background-color: white;
  padding: 20px;
  border-radius: 5px;
  box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  color: #4a7c80;
  font-size: 16px;
  text-align: center;
}
</style>
