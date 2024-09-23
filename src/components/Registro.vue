<template>
  <div class="container mt-5">
    <h2>Formulario de Registro</h2>
    <div class="mb-3">
      <label for="nombre" class="form-label">Nombre</label>
      <input type="text" id="nombre" v-model="nombre" class="form-control" @blur="validarNombre">
      <div v-if="errores.nombre" class="text-danger">{{ errores.nombre }}</div>
    </div>
    <div class="mb-3">
      <label for="correo" class="form-label">Correo</label>
      <input type="email" id="correo" v-model="correo" class="form-control" @blur="validarCorreo">
      <div v-if="errores.correo" class="text-danger">{{ errores.correo }}</div>
    </div>
    <div class="mb-3">
      <label for="password" class="form-label">Contraseña</label>
      <input type="password" id="password" v-model="password" class="form-control">
    </div>
    <div class="mb-3">
      <label for="repassword" class="form-label">Repetir Contraseña</label>
      <input type="password" id="repassword" v-model="repassword" class="form-control" @blur="validarContraseñas">
      <div v-if="errores.password" class="text-danger">{{ errores.password }}</div>
    </div>
    <button @click="registrar" class="btn btn-primary">Enviar</button>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nombre: '',
      correo: '',
      password: '',
      repassword: '',
      errores: {
        nombre: '',
        correo: '',
        password: ''
      }
    };
  },
  methods: {
    validarNombre() {
      if (!this.nombre) {
        this.errores.nombre = 'El campo nombre es requerido';
      } else {
        this.errores.nombre = '';
      }
    },
    validarCorreo() {
      const correoValido = /^[^\s@]+@[^\s@]+\.[^\s@]+$/.test(this.correo);
      if (!correoValido) {
        this.errores.correo = 'El formato del correo es incorrecto';
      } else {
        this.errores.correo = '';
      }
    },
    validarContraseñas() {
      if (this.password !== this.repassword) {
        this.errores.password = 'Las contraseñas no coinciden';
      } else {
        this.errores.password = '';
      }
    },
    registrar() {
      // Validar todos los campos antes de registrar
      this.validarNombre();
      this.validarCorreo();
      this.validarContraseñas();

      if (!this.errores.nombre && !this.errores.correo && !this.errores.password) {
        alert('El registro se ha realizado correctamente');
      }
    }
  }
};
</script>
