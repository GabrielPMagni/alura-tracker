<template>
    <section>
        <strong class="display">{{ tempoDecorrido }}</strong>
    </section>
</template>

<script lang="ts">
    import { defineComponent } from 'vue';
    export default defineComponent({
        name: 'CronometroDefault',
        computed: {
            tempoDecorrido() : string {
                return new Date(this.tempoEmSegundos * 1000).toISOString().substring(11,19)
            }
        },
        props: {
            tempoEmSegundos: {
                type: Number,
                default: 0
            }
        }
    })
</script>

<style scoped>
    .display{
        color: var(--color-primario);
    }
</style>