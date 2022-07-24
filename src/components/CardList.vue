<template>
  <div class="row">
    <div 
        class="col-12"
        v-for="pais in paises" :key="pais.name"
    >
        <Card :pais="pais" />
    </div>
  </div>
</template>

<script>
import Card from './Card'
import { computed, onMounted } from 'vue'
import {useStore} from 'vuex'  //con esta importación me traigo toda la tienda store
export default {
    components: {
        Card
    },
    setup(){
        const store = useStore()  //me traigo toda la tienda

        const paises = computed(() => {
            return store.getters.topPaisesPoblacion
        })

        onMounted(async() => {
            await store.dispatch('getPaises')   //dispatch para ejecutar una acción de la sstore
            await store.dispatch('filtrarRegion', 'Americas')
        })

        return {paises}
    }
}
</script>

<style>

</style>