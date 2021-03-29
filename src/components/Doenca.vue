<template>
  <div class="container-fluid">
    <div class="componentes">
      <app-doenca-sintoma />
      <app-doenca-resultado />
    </div>
  </div>
</template>

<script>
import AppDoencaSintoma from "./DoencaSintoma";
import AppDoencaResultado from "./DoencaResultado";

export default {
  components: { AppDoencaSintoma, AppDoencaResultado },
};
</script>

<style scoped>
.container-fluid {
  background-image: url("../img/fundo.jpg");
  background-size: 100% 100%;
  position: relative;
  width: 100%;
  height: 100vh;
  align-items: center;
  display: flex;
  flex-direction: row;
  flex-wrap: wrap;
  justify-content: center;
}

.container-fluid hr {
  margin: 20px 10px;
}

.componentes {
  display: flex;
  margin-top: 300px;
  width: 1000px;
  max-width: 1000px;
}

.componentes > * {
  margin: 10px;
}
</style>
