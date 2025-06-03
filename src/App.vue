<script setup>
  import { ref,  reactive } from 'vue'
  import { db } from './data/guitarras'
  import Guitarra from './components/Guitarra.vue'
  import Header from './components/Header.vue'
  import Footer from './components/Footer.vue'

const guitarras = ref(db)

const carrito = ref([])

const agregarCarrito = (guitarra) => {
    //Vamos a crear un elemento que compruebe si el producto ya esta en el carrito
    const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)
    
    if(existeCarrito >= 0){
        carrito.value[existeCarrito].cantidad++
    }else{
        guitarra.cantidad = 1
        carrito.value.push(guitarra)
    }
}

</script>

<template>
    <Header
    :carrito="carrito"
    />
      

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

    <Footer/>
</template>


