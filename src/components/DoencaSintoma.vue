<template>
  <div class="componente">
    <div class="sintomas">
      <h2 class="text-dark">Seleção de sintomas</h2>
      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="febre"
          v-model="febre"
        />
        <label class="form-check-label" for="flexCheckDefault"> Febre. </label>
      </div>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="dorCabeca"
          v-model="dorCabeca"
        />
        <label class="form-check-label" for="flexCheckDefault">
          Dor de cabeça.
        </label>
      </div>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="fadiga"
          v-model="fadiga"
        />
        <label class="form-check-label" for="flexCheckDefault"> Fadiga. </label>
      </div>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="perdaPaladar"
          v-model="perdaPaladar"
        />
        <label class="form-check-label" for="flexCheckDefault">
          Perda de paladar.
        </label>
      </div>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="tosseSeca"
          v-model="tosseSeca"
        />
        <label class="form-check-label" for="flexCheckDefault">
          Tosse seca.
        </label>
      </div>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="faltaAr"
          v-model="faltaAr"
        />
        <label class="form-check-label" for="flexCheckDefault">
          Falta de ar.
        </label>
      </div>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="doresCorpo"
          v-model="doresCorpo"
        />
        <label class="form-check-label" for="flexCheckDefault">
          Dores no corpo.
        </label>
      </div>

      <div class="form-check">
        <input
          class="form-check-input"
          type="checkbox"
          value=""
          id="dorGarganta"
          v-model="dorGarganta"
        />
        <label class="form-check-label" for="flexCheckDefault">
          Dor de garganta.
        </label>
      </div>

      <button
        v-if="!resultado"
        type="button"
        class="btn btn-info mt-5"
        @click="iniciarDiagnostico"
      >
        Iniciar Diagnóstico
      </button>
      <button
        v-else
        type="button"
        class="btn btn-dark mt-5"
        @click="novoDiagnostico"
      >
        Novo Diagnóstico
      </button>
    </div>
  </div>
</template>

<script>
import barramento from "@/barramento";

export default {
  data() {
    return {
      febre: false,
      dorCabeca: false,
      fadiga: false,
      perdaPaladar: false,
      tosseSeca: false,
      faltaAr: false,
      doresCorpo: false,
      dorGarganta: false,
      contador: 0,
      resultado: null,
    };
  },
  methods: {
    iniciarDiagnostico() {
      if (this.febre == true) {
        this.contador += 20;
      }
      if (this.dorCabeca == true) {
        this.contador += 7;
      }
      if (this.fadiga == true) {
        this.contador += 10;
      }
      if (this.perdaPaladar == true) {
        this.contador += 5;
      }
      if (this.tosseSeca == true) {
        this.contador += 15;
      }
      if (this.faltaAr == true) {
        this.contador += 30;
      }
      if (this.doresCorpo == true) {
        this.contador += 8;
      }
      if (this.dorGarganta == true) {
        this.contador += 5;
      }

      if (this.contador == 0) {
        this.resultado = "Nenhum sintoma selecionado.";
      }

      if (this.faltaAr == true) {
        this.resultado = `Diante dos sintomas apresentados e principalmente da falta de ar, a probabilidade é de ${this.contador}% de ser Covid-19. Procure imediatamente um posto de saúde. `;
      } else {
        if (
          this.faltaAr == false &&
          this.febre == false &&
          this.fadiga == false &&
          this.tosseSeca == false
        ) {
          this.resultado = `Diante dos sintomas apresentados, a probabilidade é de ${this.contador}% de ser Covid-19. Os sintomas são leves, caso seja uma pessoa saudável permaneça em repouso sem contato externo por pelo menos 14 dias, caso contrário procure imediatamente um posto de saúde. `;
        } else {
          this.resultado = `Diante dos sintomas apresentados, a probabilidade é de ${this.contador}% de ser Covid-19.`;
        }
      }
      
      this.desabilitarCheckboxs();
      barramento.$emit("resultadoMudou", this.resultado);
    },
    desabilitarCheckboxs() {
      document.getElementById("febre").disabled = true;
      document.getElementById("dorCabeca").disabled = true;
      document.getElementById("fadiga").disabled = true;
      document.getElementById("perdaPaladar").disabled = true;
      document.getElementById("tosseSeca").disabled = true;
      document.getElementById("faltaAr").disabled = true;
      document.getElementById("doresCorpo").disabled = true;
      document.getElementById("dorGarganta").disabled = true;
    },
    novoDiagnostico() {
      document.getElementById("febre").disabled = false;
      document.getElementById("dorCabeca").disabled = false;
      document.getElementById("fadiga").disabled = false;
      document.getElementById("perdaPaladar").disabled = false;
      document.getElementById("tosseSeca").disabled = false;
      document.getElementById("faltaAr").disabled = false;
      document.getElementById("doresCorpo").disabled = false;
      document.getElementById("dorGarganta").disabled = false;

      this.resultado = null;
      this.contador = 0;
      barramento.$emit("resultadoMudou", this.resultado);
    },
  },
};
</script>

<style scoped>
.componente {
  flex: 1;
  padding-left: 40px;
  color: rgb(10, 1, 1);
}

.sintomas {
  text-align: left;
  font-size: 1rem;
  padding-left: 15px;
}
</style>
