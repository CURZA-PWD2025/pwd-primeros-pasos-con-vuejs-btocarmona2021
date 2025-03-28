<script setup lang="ts">
import { ref } from "vue";

// Definición de variables reactivas.
const nombre = ref("");
const focusNombre = ref(false);
const email = ref("");
const focusEmail = ref(false);
const password = ref();
const focusPassword = ref(false);
const fecha = ref(new Date().toISOString().substr(0, 10));
const focusFecha = ref(false);
const passwordEncriptado = ref("");

const submitForm = () => {
if (!nombre.value || !email.value || !password.value || !fecha.value) {
    alert("Todos los campos son obligatorios");
    return;
  }
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
  focusNombre.value = false;
  focusEmail.value = false;
  focusPassword.value = false;
  focusFecha.value = false;
};
const focus = (e:FocusEvent) => {
  const target = e.target as HTMLInputElement;
  if (target.placeholder === "Nombre"){
    focusNombre.value = true;
  }else if (target.placeholder === "Email"){
    focusEmail.value = true; 
  }else if (target.placeholder === "Password"){
    focusPassword.value = true;
  }else if (target.placeholder === "Fecha"){
    focusFecha.value = true;
  }
};
</script>

<template>
  <div class="main">
    <form class="main__form" @submit.prevent="submitForm">
      <input type="text" v-model="nombre" placeholder="Nombre" @focus=focus />
      <input type="email" v-model="email" placeholder="Email" @focus=focus />
      <input
        type="password"
        v-model="password"
        @input="encriptarPassword"
        placeholder="Password"
        @focus=focus 
      />
      <input type="date" v-model="fecha" placeholder="Fecha" @focus=focus />
      <button type="submit">Enviar</button>
    </form>
    <div class="main__data">
      <p><span v-if="focusNombre">✔</span> Nombre: <span>{{ nombre }}</span></p>
      <p><span v-if="focusEmail">✔</span> Email: <span>{{ email }}</span></p>
      <p><span v-if="focusPassword">✔</span> Password:<span>{{ passwordEncriptado }}</span></p>
      <p><span v-if="focusFecha">✔</span> Edad: <span>{{ calcularEdad() }} año/s</span></p>

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
  outline: none;
}
input:focus-within {
  outline-color: rgb(63, 0, 88) 2px solid;
  box-shadow: 0 0 10px 10px rgba(94, 71, 133);
  outline: rgb(171, 0, 238) 2px solid; ;
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
span {
  font-weight: bold;
  color:  rgb(171, 0, 238);
}
</style>
