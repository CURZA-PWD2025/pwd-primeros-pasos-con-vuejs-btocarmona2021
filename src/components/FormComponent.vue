<script setup lang="ts">
import { ref } from 'vue';

const nombre = ref("");
const email = ref("");
const password = ref();
const fecha = ref("");

const submitForm = () => {

  const usuario = {
    nombre: nombre.value,
    email: email.value,
    password: password.value,
    edad: calcularEdad(),
  };
  alert(JSON.stringify(usuario));
  limpiarForm();
};

const calcularEdad = ( )=> {
  const fechaNacimiento = new Date(fecha.value);
  const hoy = new Date();
  const edad = hoy.getFullYear() - fechaNacimiento.getFullYear();
  return edad;
};

const limpiarForm = () => {
  nombre.value = "";
  email.value = "";
  password.value = "";
  fecha.value = "";
};
</script>

<template>
  <form class="form" @submit.prevent="submitForm">
    <input type="text" v-model="nombre" placeholder="Nombre" />
    <input type="email" v-model="email" placeholder="Email" />
    <input type="password" v-model="password" placeholder="Password" />
    <input type="date" v-model="fecha" />
    <button type="submit">Enviar</button>
  </form>
</template>

<style scoped>
.form {
  display: flex;
  width: 300px;
  padding: 20px;
  background-color: #222222;
  box-shadow: 0 0 10px 10px rgba(94, 71, 133, 0.2);
  flex-direction: column;
  border-radius: 8px;
  gap: 1rem;
}
input {
  padding: 10px;
  border-radius: 8px;
  border: none;
  margin-bottom: 1rem;
  font-family: "Chakra Petch", sans-serif;
  font-size: 1.1rem;
}
</style>
