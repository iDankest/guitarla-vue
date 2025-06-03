<script setup>
  import { ref,  reactive, onMounted } from 'vue'
  import { db } from './data/guitarras'
  import Guitarra from './components/Guitarra.vue'
  import Header from './components/Header.vue'
  import Footer from './components/Footer.vue'

const guitarras = ref(db)
const guitarra = ref({})

const carrito = ref([])
onMounted(() => {
    guitarra.value = guitarras.value[3]
})
const agregarCarrito = (guitarra) => {
    //Vamos a crear un elemento que compruebe si el producto ya esta en el carrito
    const existeCarrito = carrito.value.findIndex(producto => producto.id === guitarra.id)
    
    if(existeCarrito >= 0){//Aqui evita que se repita el producto
        carrito.value[existeCarrito].cantidad++
    }else{
        guitarra.cantidad = 1
        carrito.value.push(guitarra)
    }
}

const decrementarCantidad = (id) => {
    const index = carrito.value.findIndex(producto => producto.id === id)
    if(carrito.value[index].cantidad <= 1) return //Evita que se pase de 1
    carrito.value[index].cantidad--
}

const incrementarCantidad = (id) => {
    const index = carrito.value.findIndex(producto => producto.id === id)
    if(carrito.value[index].cantidad >= 5) return //Evita que se pase de 5
    carrito.value[index].cantidad++
}
const eleminarProducto = (id) => {
    // const index = carrito.value.findIndex(producto => producto.id === id)
    // carrito.value.splice(index, 1)
    carrito.value = carrito.value.filter(producto => producto.id !== id)
}
const vaciarCarrito = () => {
    carrito.value = []
}

</script>

<template>
    <Header
    :carrito="carrito"
    :guitarra="guitarra"
    @eleminar-producto="eleminarProducto"
    @vaciar-carrito="vaciarCarrito"
    @decrementar-cantidad="decrementarCantidad"
    @incrementar-cantidad="incrementarCantidad"
    @agregar-carrito="agregarCarrito"
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


