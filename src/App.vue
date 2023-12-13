<script setup>
  import { ref } from "vue";

  const showModal = ref(false);
  const newNote = ref("");
  const notes = ref([]);
  const errorMessage = ref("");

  function getRandomColor() {
    return "hsl(" + Math.random() * 360 + ", 100%, 75%)";
  }

  const addNote = () => {
    if (newNote.value.length <= 0) return errorMessage.value = "Note can't be empty."
    notes.value.push({
      id: Math.floor(Math.random() * 1000),
      text: newNote.value,
      date: new Date().toLocaleString('en-GB', { dateStyle: "short" }),
      backgroundColor: getRandomColor(),
    })
    showModal.value = false;
    newNote.value = "";
    errorMessage.value = "";
  }

</script>

<template>
  <main>
    <div v-if="showModal" class="overlay">
      <div class="modal">
        <p @click="showModal = false" class="closeModalBtn">x</p>
        <textarea v-model.trim="newNote" name="note" id="note" cols="30" rows="10" ></textarea>
        <p v-show="errorMessage">{{ errorMessage }}</p>
        <button @click="addNote">Add Note</button>
      </div>
    </div>
    <div class="container">
      <header>
        <h1>Notes</h1>
        <button @click="showModal = true">+</button>
      </header>
      <div class="cards-container">
        <div
          v-for="note in notes"
          class="card"
          :style="{backgroundColor: note.backgroundColor}"
          :key="note.id"
        >
          <p class="main-text">{{ note.text }}</p>
          <p class="date">{{ note.date }}</p>
        </div>
      </div>
    </div>
  </main>
</template>

<style scoped>
  .container {
    max-width: 1000px;
    padding: 10px;
    margin: 0 auto
  }

  h1 {
    font-weight: bold;
    margin-bottom: 25px;
    font-size: 75px;
  }

  .card {
    width: 225px;
    height: 225px;
    background-color: rgb(237, 182, 44);
    padding: 12px 16px;
    border-radius: 15px;
    display: flex;
    flex-direction: column;
    justify-content: space-between;
    margin-right: 20px;
    margin-bottom: 20px;
  }

  .main-text {
    line-height: 1.25;
    font-size: 17.5px;
    font-weight: bold;
  }

  .date {
    font-size: 12.5px;
    margin-top: auto;
  }

  header {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }

  header button {
    border: none;
    padding: 10px;
    width: 50px;
    height: 50px;
    cursor: pointer;
    background-color: var(--vt-c-white-soft);
    border-radius: 1000px;
    color: var(--vt-c-text-light-1);
    font-size: 20px;
    box-shadow: 1px 1px 10px #00000035;
  }

  .card {
    color: var(--vt-c-text-light-1);
  }

  .cards-container {
    display: flex;
    flex-wrap: wrap;
  }

  .overlay {
    position: absolute;
    width: 100%;
    height: 100%;
    background-color: rgba(0, 0, 0, 0.77);
    transform: translate(-50%, -50%);
    top: 50%;
    left: 50%;
    display: flex;
    align-items: center;
    justify-content: center;
    z-index: 10;
  }

  main {
    height: 100vh;
    width: 100vw;
  }

  .modal {
    width: 750px;
    background-color: white;
    border-radius: 10px;
    padding: 30px;
    position: relative;
    display: flex;
    flex-direction: column;
  }

  .modal button {
    padding: 10px 20px;
    font-size: 20px;
    width: 100%;
    background-color: blueviolet;
    border: none;
    color: white;
    cursor: pointer;
    margin-top: 15px;

  }

  .modal p {
    color: red;
  }

  textarea {
    width: 100%;
    height: 200px;
    padding: 5px;
    font-size: 20px;
  }

  .closeModalBtn {
    margin-left: auto;
    font-size: 20px;
    z-index: 11;
    cursor: pointer;
    color: var(--vt-c-text-light-1) !important;
    position: absolute;
    right: 12px;
    top: 0;
  }
</style>