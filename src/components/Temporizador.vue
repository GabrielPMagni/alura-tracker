<template>
    <div class="is-flex is-align-items-center is-justify-content-space-between">
        <CronometroDefault :tempoEmSegundos="tempoEmSegundos" />
        <button class="button" @click="iniciar" :disabled="cronometroRodando">
            <span class="icon">
                <i class="fas fa-play"></i>
            </span>
            <span>play</span>
        </button>
        <button class="button" @click="finalizar" :disabled="!cronometroRodando">
            <span class="icon">
                <i class="fas fa-stop"></i>
            </span>
            <span>stop</span>
        </button>
    </div>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    import CronometroDefault from './Cronometro.vue';
    export default defineComponent({
        name: 'TemporizadorDefault',
        emits: ['aoTemporizadorFinalizado'],
        data () {
            return {
                tempoEmSegundos: 0,
                cronometro: 0,
                cronometroRodando: false,
            }
        },
        methods: {
            iniciar () {
                this.cronometro = setInterval(() => {
                    this.tempoEmSegundos++
                }, 1000)
                this.cronometroRodando = true
            },
            finalizar () {
                clearInterval(this.cronometro)
                this.cronometroRodando = false
                this.$emit('aoTemporizadorFinalizado', this.tempoEmSegundos)
                this.tempoEmSegundos = 0
            }
        },
        components: {
            CronometroDefault
        },
    })
</script>

<style>

</style>