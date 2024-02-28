<script setup>
import { computed, ref } from "vue";

const listeContact = ref([
  {
    name: "Félix Laviéville",
    phone: "+33.6.06.06.06.06",
  },
]);

const inputName = ref("");
const inputPhone = ref("");
const inputSearch = ref("");

function ajouterContact() {
  listeContact.value.push({
    name: inputName.value,
    phone: inputPhone.value,
  });
  inputName.value = "";
  inputPhone.value = "";
}

const listeContactFiltree = computed(() => {
  return listeContact.value.filter((contact) => {
    return contact.name.includes(inputSearch.value);
  });
});
</script>

<template>
  <h1>Liste des contacts</h1>
  <main>
    <div class="formulaire">
      <input v-model="inputName" type="text" placeholder="Nom du contact" />
      <input v-model="inputPhone" type="text" placeholder="Numéro" />

      <button @click="ajouterContact">Ajouter un contact</button>
    </div>

    <input
      v-model="inputSearch"
      class="search"
      type="text"
      placeholder="Rechercher un contact..."
    />

    <div class="liste">
      <div class="contact" v-for="contact in listeContactFiltree">
        <h3>{{ contact.name }}</h3>
        <p>{{ contact.phone }}</p>
      </div>
    </div>
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

div.formulaire {
  display: flex;
  gap: 10px;
  padding-bottom: 20px;
  margin-bottom: 20px;
  border-bottom: 1px solid black;
}

input {
  border: none;
  background-color: rgb(224, 224, 224);
  padding: 10px 15px;
  border-radius: 5px;
}

input.search {
  margin-bottom: 20px;
  display: block;
  width: 100%;
  max-width: 50vw;
}

div.formulaire > button {
  border: none;
  background-color: rgb(49, 36, 78);
  padding: 10px 15px;
  border-radius: 50px;
  color: white;
}

div.contact {
  display: grid;
  grid-template-columns: 1fr 150px;
  border: 1px solid gray;
  padding: 20px;
  gap: 50px;
  align-items: center;
  margin-bottom: 20px;
}

div.contact > h3 {
  border-right: 1px solid gray;
}
</style>
