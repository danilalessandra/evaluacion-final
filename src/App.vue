<template>
  <div>
    <nav class="navbar navbar-expand-lg navbar-light bg-light">
      <div class="container-fluid">
        <a class="navbar-brand" href="#">Mi Proyecto</a>
        <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
          <span class="navbar-toggler-icon"></span>
        </button>
        <div class="collapse navbar-collapse" id="navbarNav">
          <ul class="navbar-nav">
            <li class="nav-item">
              <a class="nav-link" href="#" @click="showTab('calificaciones')">Cálculo de Calificaciones</a>
            </li>
            <li class="nav-item">
              <a class="nav-link" href="#" @click="showTab('registro')">Formulario de Registro</a>
            </li>
          </ul>
        </div>
      </div>
    </nav>

    <!-- Contenido de las pestañas -->
    <div v-if="activeTab === 'calificaciones'">
      <calificaciones></calificaciones>
    </div>
    <div v-else>
      <registro></registro>
    </div>
  </div>
</template>

<script>
import Calificaciones from './components/Calificaciones.vue';
import Registro from './components/Registro.vue';

export default {
  components: {
    Calificaciones,
    Registro
  },
  data() {
    return {
      activeTab: 'calificaciones' // Tab predeterminada
    };
  },
  methods: {
    showTab(tab) {
      this.activeTab = tab;
    }
  }
};
</script>