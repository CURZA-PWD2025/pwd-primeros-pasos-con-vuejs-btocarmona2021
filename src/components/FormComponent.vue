<script setup lang="ts">
import { ref } from "vue";

const nombre = ref("");
const email = ref("");
const password = ref();
const fecha = ref(new Date().toISOString().substr(0, 10));
const passwordEncriptado = ref("");

const submitForm = () => {
  const usuario = {
    nombre: nombre.value,
    email: email.value,
    password: password.value,
    edad: calcularEdad(),
  };
  alert(`Usuario creado correctamente: ${JSON.stringify(usuario)}`);
  limpiarForm();
};

const encriptarPassword = () => {
  passwordEncriptado.value = password.value
    .split("")
    .map((letra: string) => letra.replace(letra, "🔐"))
    .join("");
};

const calcularEdad = () => {
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
  <div class="main">
    <form class="main__form" @submit.prevent="submitForm">
      <input type="text" v-model="nombre" placeholder="Nombre" />
      <input type="email" v-model="email" placeholder="Email" />
      <input
        type="password"
        v-model="password"
        @input="encriptarPassword"
        placeholder="Password"
      />
      <input type="date" v-model="fecha" />
      <button type="submit">Enviar</button>
    </form>
    <div class="main__data">
      <p>Nombre: {{ nombre }}</p>
      <p>Email: {{ email }}</p>
      <p>Password:{{ passwordEncriptado }}</p>
      <p>Edad: {{ calcularEdad() }} años</p>
    </div>
  </div>
</template>

<style scoped>
.main {
  display: flex;
  gap: 2rem;
  justify-content: center;
  align-items: center;
  height: 100vh;
}

.main__form {
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
.main__data {
  display: flex;
  flex-direction: column;
  width: 300px;
  margin-top: 1rem;
  padding: 20px;
  background-color: #222222;
  box-shadow: 0 0 10px 10px rgba(94, 71, 133, 0.2);
  border-radius: 8px;
  font-family: "Chakra Petch", sans-serif;
  font-size: 1.1rem;
}
</style>
