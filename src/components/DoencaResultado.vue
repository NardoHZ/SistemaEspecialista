<template>
  <div class="componente">
    <h2 class="text-dark">Resultado do diagnóstico</h2>
    <div class="resultado">
      <p v-if="!resultado">Aguardando informações...</p>
      <p v-else>{{ resultado }}</p>
    </div>
  </div>
</template>

<script>
import barramento from "@/barramento";

export default {
  data() {
    return {
      resultado: null,
    };
  },
  created() {
    barramento.$on("resultadoMudou", (resultado) => {
      this.resultado = resultado;
    });
  },
};
</script>

<style scoped>
.componente {
  flex: 1;
  color: rgb(7, 0, 0);
}
.resultado {
  padding-top: 40px;
  font-size: 1.5rem;
}
</style>
