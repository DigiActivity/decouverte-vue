<script setup>
import { ref } from "vue";

const listeContact = ref([
  {
    name: "Félix Laviéville",
    phone: "+33.6.06.06.06.06",
  },
]);

const inputName = ref("");
const inputPhone = ref("");

function ajouterContact() {
  listeContact.value.push({
    name: inputName.value,
    phone: inputPhone.value,
  });
}
</script>

<template>
  <h1>Liste des contacts</h1>
  <main>
    <div class="list-contact"></div>

    <pre>{{ listeContact }}</pre>

    <input v-model="inputName" type="text" placeholder="Nom du contact" />
    <input v-model="inputPhone" type="text" placeholder="Numéro" />

    <button @click="ajouterContact">Ajouter un contact</button>
  </main>
</template>

<style>
* {
  padding: 0;
  margin: 0;
  box-sizing: border-box;
}

main {
  padding: 20px;
}

h1 {
  font-family: Arial, Helvetica, sans-serif;
  background-color: rgb(49, 36, 78);
  color: white;
  padding: 20px 30px;
}
</style>
