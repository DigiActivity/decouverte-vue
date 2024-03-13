<script setup>
import { computed, ref } from "vue";

const listeContact = ref([
  {
    id: 1,
    name: "Félix Laviéville",
    phone: "+33.6.06.06.06.06",
  },
  {
    id: 2,
    name: "Tutu",
    phone: "+33.6.06.827624",
  },
  {
    id: 3,
    name: "Zizou",
    phone: "+9387535",
  },
  {
    id: 4,
    name: "AAAAA",
    phone: "9284724",
  },
]);

const inputName = ref("");
const inputPhone = ref("");
const inputSearch = ref("");

const compteurContact = ref(4);

function ajouterContact() {
  if (inputName.value === "" || inputPhone.value === "") {
    return;
  }

  compteurContact.value++;

  listeContact.value.push({
    id: compteurContact.value,
    name: inputName.value,
    phone: inputPhone.value,
  });

  inputName.value = "";
  inputPhone.value = "";
}

function supprimeContact(idASupprimer) {
  listeContact.value = listeContact.value.filter((contact) => {
    return contact.id !== idASupprimer;
  });
}

// On veut une liste qui prenne en compte la recherche
const listeContactFiltree = computed(() => {
  // La computed() va s'actualiser automatiquement dès qu'une ref
  // (ou une autre computed) incluse dans la fonction, est mise à jour.
  return listeContact.value.filter((contact) => {
    // .filter() va parcourir le tableau
    // pour un élément donné, il vérifie quelque chose (true / false)
    // si true, alors l'élément est gardé, sinon, il est abandonné
    const nomAComparer = contact.name.toLowerCase();
    const rechercheAComparer = inputSearch.value.toLowerCase();
    return nomAComparer.includes(rechercheAComparer);
  });
});

// on veut trier par ordre alphabétique
const listeContactFiltreeOrdonnee = computed(() => {
  return listeContactFiltree.value.toSorted((contact1, contact2) => {
    if (contact1.name < contact2.name) {
      return -1;
    } else {
      return 1;
    }
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
      <div class="contact" v-for="contact in listeContactFiltreeOrdonnee">
        <h3>[{{ contact.id }}] {{ contact.name }}</h3>
        <p>{{ contact.phone }}</p>
        <button @click="supprimeContact(contact.id)">Supprimer</button>
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
  grid-template-columns: 1fr 150px auto;
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
