<script setup>
  import { ref,  reactive } from 'vue'
  import { db } from './data/guitarras'
  import Guitarra from './components/Guitarra.vue'

const guitarras = ref(db)

const carrito = ref([])

const agregarCarrito = (guitarra) => {
    carrito.value.push(guitarra)
}

</script>

<template>
      

    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <Guitarra
                v-for="guitarra in guitarras"
                :guitarra="guitarra"
                @agregar-carrito="agregarCarrito" 
                
            />
            <!-- Estamos importando el evento del componente a este otro componente -->
        </div>
    </main>


</template>


