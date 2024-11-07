<script setup>
import { ref } from 'vue'

const entries = ref([]) // Array to store entries
const description = ref('') // Model for "Keterangan" input
const amount = ref('') // Model for "Jumlah Uang" input

// Function to submit a new entry
const submitEntry = () => {
  if (description.value && amount.value) {
    entries.value.push({
      id: Date.now(),
      description: description.value,
      amount: parseFloat(amount.value),
    })
    description.value = ''
    amount.value = ''
  }
}

// Function to delete a specific entry
const deleteEntry = (id) => {
  entries.value = entries.value.filter(entry => entry.id !== id)
}

// Function to delete all entries
const clearAllEntries = () => {
  entries.value = []
}
</script>

<template>
  <div class="arsip-dompetku">
    <h2>Arsip Dompetku</h2>

    <div class="input-group">
      <label for="description">Keterangan:</label>
      <input id="description" v-model="description" placeholder="Masukkan keterangan" />

      <label for="amount">Jumlah Uang (in/out):</label>
      <input id="amount" v-model="amount" type="number" placeholder="Masukkan jumlah uang" />

      <button @click="submitEntry">Submit</button>
    </div>

    <div v-if="entries.length" class="entry-list">
      <h3>Daftar Transaksi</h3>
      <ul>
        <li v-for="entry in entries" :key="entry.id">
          <span>{{ entry.description }} - Rp{{ entry.amount.toLocaleString() }}</span>
          <button @click="deleteEntry(entry.id)">Delete</button>
        </li>
      </ul>
      <button @click="clearAllEntries" class="clear-button">Delete All</button>
    </div>
    <p v-else>Tidak ada transaksi</p>
  </div>
</template>

<ArsipDompetku style="margin-bottom: 50px;" />

<style scoped>
.large-spacing {
  margin-bottom: 50px; /* Adjust as needed */
}
</style>

<style scoped>
.arsip-dompetku {
  max-width: 650px;
  margin: 0 auto;
  padding: 1rem;
  background-color: #f9f9f9;
  border: 1px solid #ddd;
  border-radius: 8px;
}

h2 {
  text-align: center;
  font-size: 1.8rem;
  color: #333;
}

.input-group {
  display: flex;
  flex-direction: column;
  gap: 1rem;
  margin-bottom: 1rem;
}

label {
  font-weight: bold;
}

input {
  padding: 0.5rem;
  border: 1px solid #ccc;
  border-radius: 4px;
}

button {
  padding: 0.5rem;
  color: #fff;
  background-color: #28a745;
  border: none;
  border-radius: 4px;
  cursor: pointer;
  font-weight: bold;
}

button:hover {
  background-color: #218838;
}

.entry-list {
  margin-top: 1rem;
}

.entry-list h3 {
  text-align: center;
}

ul {
  list-style-type: none;
  padding: 0;
}

li {
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 0.5rem 0;
  border-bottom: 1px solid #ddd;
}

li button {
  padding: 0.3rem;
  background-color: #dc3545;
}

li button:hover {
  background-color: #c82333;
}

.clear-button {
  width: 100%;
  margin-top: 1rem;
  background-color: #dc3545;
}

.clear-button:hover {
  background-color: #c82333;
}
</style>
