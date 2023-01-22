<script setup>
import { ref } from 'vue'

const notes = ref([])
const IsNewNotesDiv = ref(false)
let newNotebody = ref('')

const createNote = (body) => {
  notes.value.push({
    id: Date.now(),
    body: body,
    backgroundColor: getRandomColor()
  })
  displayNewNoteDiv()
  newNotebody.value = ''
}

const displayNewNoteDiv = () => {
  IsNewNotesDiv.value = !IsNewNotesDiv.value
}

const getRandomColor = () => {
  return "hsl(" + Math.random() *   360 + ", 100%, 70%)";
}


</script>

<template>

  <header>
    <h1>Notes</h1>
    <button @click="displayNewNoteDiv()">+</button>
  </header>

  <div class="new-notes-div" v-if="IsNewNotesDiv" >
    <input type="text" v-model="newNotebody" />
    <button class="btn-add-note" @click="createNote(newNotebody)">add Note</button>
  </div>

  <ul>
    <li v-for="note in notes" :key="note.id" :style="{ 'background-color': note.backgroundColor}">
      <p class="text">{{ note.body }}</p> <p class="text">{{ note.id }}</p> 
    </li>
  </ul>
</template>

<style scoped>
header{
  display: flex;
  justify-content: space-between;
  align-items: center;
  padding: 3em 8em;
}

button {
  background-color: #4CAF50;
  /* make rounded btn */
  border: none;
  color: white;
  border-radius: 50%;
  padding: 0.5rem 0.75rem;
  text-align: center;
  text-decoration: none;
  font-size: 1.5rem;
  margin: 1em;
}

.new-notes-div{
  /*display above everything*/
  position: absolute;
  top: 0;
  left: 0;
  width: 100vw;
  height: 100vh;
  background-color: rgba(0,0,0,0.5);
  z-index: 1;
  display: flex;
  justify-content: center;
  align-items: center;
  
}

ul {
  display: row;
  list-style: none;
  padding: 0;
  margin: 3em;
  gap: 2em;
  
}
li{
  display: flex;
  flex-direction: column;
  justify-content: space-between;
  margin: 1em 0;
  padding: 0.5em 3em 0.5em 0.5em;
  color: rgb(24, 24, 24);
  gap: 6em;
}

.btn-add-note{
  margin: 0em;
  padding: 0.3em;

  border-radius: 8%;
}
.text{
  font-weight: bold;
}

input{
  margin: 1em;
  padding: 0em 5em 5em 0em;
}

h1 {
  text-align: center;
  display: block;
}
</style>
