<script>
import contacts from "./contacts.json";

export default {
  data() {
    return {
      AllContacts: contacts,
      visibleContacts: contacts.slice(0, 5),
    };
  },
  computed: {},
  methods: {
    createNewContact() {
      let randomNumber = Math.floor(Math.random() * (52 - 5)) + 5;
      let randomContact = this.AllContacts[randomNumber];
      console.log(randomContact);

      if (this.AllContacts.includes(randomContact)) {
        //Qué hacer para que no se repitan los números random
      }
      return this.visibleContacts.push(randomContact);
    },
    filterByPop() {
      this.visibleContacts.sort((contact1, contact2) => {
        if (contact1.popularity > contact2.popularity) {
          return -1;
        }
        if (contact1.popularity < contact2.popularity) {
          return 1;
        }
        return 0;
      });
    },
    filterByName() {
      this.visibleContacts.sort((contact1, contact2) => {
        if (contact1.name.toLowerCase() > contact2.name.toLowerCase()) {
          return 1;
        }
        if (contact1.name.toLowerCase() < contact2.name.toLowerCase()) {
          return -1;
        }
        return 0;
      });
    },
    DeleteContact() {},
  },
};
</script>

<!-- HTML de la APP-->
<template>
  <div id="app">
    <h1>Contactos Singulares</h1>
    <button @click="createNewContact">Add Random Contact</button>
    <button @click="filterByName">Filter by Name</button>
    <button @click="filterByPop">Filter by Popularity</button>
    <table>
      <thead>
        <tr>
          <th>Picture</th>
          <th>Name</th>
          <th>Popularity</th>
          <th>Won an Oscar</th>
          <th>Won an Emy</th>
        </tr>
      </thead>
      <tbody>
        <tr v-for="contact in visibleContacts" :key="contact.id">
          <td>
            <img style="width: 100px" :src="contact.pictureUrl" />
          </td>
          <td>{{ contact.name }}</td>
          <td>{{ contact.popularity.toFixed(2) }}</td>
          <td v-if="contact.wonOscar">
            <img
              src="https://github.githubassets.com/images/icons/emoji/unicode/1f3c6.png"
              alt="Oscar"
            />
          </td>
          <td v-else></td>
          <td v-if="contact.wonEmmy">
            <img
              src="https://github.githubassets.com/images/icons/emoji/unicode/1f3c6.png"
              alt="Emy"
            />
          </td>
          <td v-else></td>
          <td>
            <button @click="DeleteContact">Delete</button>
          </td>
        </tr>
      </tbody>
    </table>
  </div>
</template>


<!-- estilos globales de la aplicación -->
<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
  margin-top: 60px;
}
</style>
