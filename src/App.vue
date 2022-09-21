<template>
  <main class="columns is-gapless is-multiline" :class="{ 'modo-escuro': modoEscuroAtivo }">
    <div class="column is-one-quarter">
      <BarraLateral @aoTemaAlterado="toggleTemaNoturno"/>
    </div>
    <div class="column is-three-quarter conteudo">
      <Formulario @aoSalvarTarefa="salvarTarefa" />
      <div class="lista">
        <Tarefa v-for="(tarefa, index) in tarefas" :key="index" :tarefa="tarefa" />
        <Box v-if="listaEstaVazia">
          Você não está muito produtivo hoje :(
        </Box>
      </div>
    </div>
  </main>
</template>

<script lang="ts">
  import { defineComponent } from 'vue';
  import Formulario from '@/components/Formulario.vue'
  import BarraLateral from '@/components/BarraLateral.vue';
  import ITarefa from '@/components/interfaces/ITarefa';
  import Tarefa from '@/components/Tarefa.vue';
  import Box from '@/components/Box.vue';
    export default defineComponent({
      name: "App",
      data () {
        return {
          tarefas: [] as ITarefa[],
          modoEscuroAtivo: false
        }
      },
      computed: {
        listaEstaVazia () : boolean {
          return this.tarefas.length === 0
        }
      },
      methods: {
        salvarTarefa(tarefa: ITarefa) {
          this.tarefas.push(tarefa)
        },
        toggleTemaNoturno(isTemaEscuro: boolean) {
          this.modoEscuroAtivo = isTemaEscuro
        }
      },
      components: { BarraLateral, Formulario, Tarefa, Box }
  });
</script>

<style>
  main {
    --bg-primario: #fff;
    --color-primario: #000;
  }
  main.modo-escuro {
    --bg-primario: #2b2d42;
    --color-primario: #ddd;  
  }
  .conteudo {
    background-color: var(--bg-primario);
  }
</style>
