<template>
    <div class="box">
        <div class="columns">
            <div class="column is-8" role="form" aria-label="Formulário para criação de uma nova tarefa">
                <input type="text" class="input" placeholder="Qual tarefa você deseja iniciar?" v-model="descricao" />
            </div>
            <div class="column">
                <Temporizador @aoTemporizadorFinalizado="finalizarTarefa" />
            </div>
        </div>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    import Temporizador from '@/components/Temporizador.vue';
import ITarefa from './interfaces/ITarefa';
    export default defineComponent({
        name: 'FormularioDefault',
        data () {
            return {
                descricao: ''
            }
        },
        emits: [ 'aoSalvarTarefa' ],
        components: {
            Temporizador, 
        },
        methods: {
            finalizarTarefa(tempoDecorrido: number) : void {
                this.$emit('aoSalvarTarefa', { duracaoEmSegundos: tempoDecorrido, descricao: this.descricao } as ITarefa)
                this.descricao = ''
            }
        }
    })
</script>

<style>
    .lista {
        padding: 1.25rem;
    }
</style>