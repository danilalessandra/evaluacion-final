<template>
  <div class="container mt-5">
    <h2>Cálculo de Calificaciones</h2>
    <div class="mb-3">
      <label for="nota1" class="form-label">Nota 1 (35%)</label>
      <input type="number" id="nota1" v-model="nota1" @blur="validarNota1" min="10" max="70" class="form-control">
      <div v-if="errores.nota1" class="text-danger">{{ errores.nota1 }}</div>
    </div>
    <div class="mb-3">
      <label for="nota2" class="form-label">Nota 2 (35%)</label>
      <input type="number" id="nota2" v-model="nota2" @blur="validarNota2" min="10" max="70" class="form-control">
      <div v-if="errores.nota2" class="text-danger">{{ errores.nota2 }}</div>
    </div>
    <div class="mb-3">
      <label for="nota3" class="form-label">Nota 3 (30%)</label>
      <input type="number" id="nota3" v-model="nota3" @blur="validarNota3" min="10" max="70" class="form-control">
      <div v-if="errores.nota3" class="text-danger">{{ errores.nota3 }}</div>
    </div>
    <div class="mb-3">
      <label for="asistencia" class="form-label">Asistencia (%)</label>
      <input type="number" id="asistencia" v-model="asistencia" @blur="validarAsistencia" min="0" max="100" class="form-control">
      <div v-if="errores.asistencia" class="text-danger">{{ errores.asistencia }}</div>
    </div>
    <button @click="calcularPromedio" class="btn btn-primary">Calcular</button>
    
    <div v-if="resultado" :class="resultado.aprobado ? 'text-success' : 'text-danger'">
      <h3>{{ resultado.mensaje }}</h3>
    </div>
  </div>
</template>

<script>
export default {
  data() {
    return {
      nota1: 0,
      nota2: 0,
      nota3: 0,
      asistencia: 0,
      errores: {
        nota1: '',
        nota2: '',
        nota3: '',
        asistencia: ''
      },
      resultado: null
    };
  },
  methods: {
    validarNota1() {
      if (this.nota1 < 10) {
        this.errores.nota1 = 'El valor debe ser superior o igual a 10';
      } else if (this.nota1 > 70) {
        this.errores.nota1 = 'El valor debe ser inferior o igual a 70';
      } else {
        this.errores.nota1 = '';
      }
    },
    validarNota2() {
      if (this.nota2 < 10) {
        this.errores.nota2 = 'El valor debe ser superior o igual a 10';
      } else if (this.nota2 > 70) {
        this.errores.nota2 = 'El valor debe ser inferior o igual a 70';
      } else {
        this.errores.nota2 = '';
      }
    },
    validarNota3() {
      if (this.nota3 < 10) {
        this.errores.nota3 = 'El valor debe ser superior o igual a 10';
      } else if (this.nota3 > 70) {
        this.errores.nota3 = 'El valor debe ser inferior o igual a 70';
      } else {
        this.errores.nota3 = '';
      }
    },
    validarAsistencia() {
      if (this.asistencia < 0 || this.asistencia > 100) {
        this.errores.asistencia = 'Por favor ingrese un valor entre 0 y 100';
      } else {
        this.errores.asistencia = '';
      }
    },
    calcularPromedio() {
      // Validar que no existan errores antes de calcular
      if (this.errores.nota1 || this.errores.nota2 || this.errores.nota3 || this.errores.asistencia) {
        this.resultado = { aprobado: false, mensaje: 'Por favor ingrese los valores válidos para las notas y la asistencia' };
        return;
      }

      const promedio = this.nota1 * 0.35 + this.nota2 * 0.35 + this.nota3 * 0.30;

      if (promedio >= 40 && this.asistencia >= 80) {
        this.resultado = { aprobado: true, mensaje: `Aprobado con un promedio de ${promedio.toFixed(2)}` };
      } else {
        this.resultado = { aprobado: false, mensaje: `Reprobado con un promedio de ${promedio.toFixed(2)}` };
      }
    }
  }
};
</script>
