<template>
  <button @click="showModal = true">Agregar Movimiento</button>
  <teleport to="#app">
    <modal-cash v-show="showModal" @close="showModal = false">
      <form @submit.prevent="submit">
        <div class="field">
          <label>Titulo</label>
          <input type="text" v-model="title" />
        </div>
        <div class="field">
          <label>Monto</label>
          <input type="number" v-model="amount" />
        </div>
        <div class="field">
          <label>Descripción</label>
          <textarea rows="4" v-model="Description"></textarea>
        </div>
        <div class="field">
          <label class="radio-label">
            <input type="radio" v-model="movementType" value="Ingreso" />
            <span>Ingreso</span>
          </label>
        </div>
        <div class="field">
          <label class="radio-label">
            <input type="radio" v-model="movementType" value="Gasto" />
            <span>Gasto</span>
          </label>
        </div>
        <div class="action">
          <button>Agregar Movimiento</button>
        </div>
      </form>
    </modal-cash>
  </teleport>
</template>
<script setup>
import { ref } from "vue";
import ModalCash from "./ModalCash.vue";

const showModal = ref(false);
const title = ref("");
const amount = ref(0);
const Description = ref("");
const movementType = ref("ingreso");
</script>

<style scoped>
button {
  color: white;
  font-size: 1.25rem;
  background-color: var(--brand-blue);
  border: none;
  width: 100%;
  padding: 24px 60px;
  border-radius: 60px;
  box-sizing: border-box;
}

form {
  font-size: 1.24rem;
  width: 100%;
}

form .action {
  padding: 0 24px;
}

.field {
  display: flex;
  justify-content: space-between;
  flex-direction: column;
  padding: 16px 24px;
}

label {
  margin-bottom: 8px;
}

input,
textarea {
  font-size: 1.24rem;
  border: 2px solid var(--brand-blue);
  border-radius: 8px;
  padding: 8px;
}

input[type="number"] {
  text-align: right;
}

.radio-label {
  display: flex;
  align-items: center;
  margin-top: 8px;
}

.radio-label span {
  margin-top: 4px;
  margin-left: 8px;
}

input[type="radio"] {
  appearance: none;
  width: 1.24rem;
  height: 1.24rem;
  color: var(--brand-blue);
  border: 2px solid var(--brand-blue);
  border-radius: 50%;
}

input[type="radio"]:checked {
  background-color: var(--brand-blue);
}
</style>
