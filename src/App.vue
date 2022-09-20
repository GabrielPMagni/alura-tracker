<template>
  <main class="columns is-gapless is-multiline">
    <div class="column is-one-quarter">
      <BarraLateral/>
    </div>
    <div class="column is-three-quarter">
      <Formulario @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
      </div>
    </div>
  </main>
</template>

<script lang="ts">
  import { defineComponent } from 'vue';
  import Formulario from '@/components/Formulario.vue'
  import BarraLateral from '@/components/BarraLateral.vue';
import ITarefa from './components/interfaces/ITarefa';
import Tarefa from './components/Tarefa.vue';
    export default defineComponent({
      name: "App",
      data () {
        return {
          tarefas: [] as ITarefa[]
        }
      },
      methods: {
        salvarTarefa(tarefa: ITarefa) {
          this.tarefas.push(tarefa)
          console.log(this.tarefas);
          
        }
      },
      components: { BarraLateral, Formulario, Tarefa }
  });
</script>

<style>
</style>
