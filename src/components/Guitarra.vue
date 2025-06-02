<script setup>
const props = defineProps({
    guitarra: {
        type: Object,
        required: true
    }
})
defineEmits(['agregar-carrito']) //Aqui declaramos el evento
</script>
<template>
            <div class="col-md-6 col-lg-4 my-4 row align-items-center">
                <div class="col-4">
                    <img class="img-fluid" :src="`/img/${guitarra.imagen}.jpg`" :alt="'imagen guitarra ' + guitarra.nombre">
                </div>
                <div class="col-8">
                    <h3 class="text-black fs-4 fw-bold text-uppercase">{{ guitarra.nombre }}</h3>
                    <p>{{ guitarra.descripcion }}</p>
                    <p class="fw-black text-primary fs-3">${{ guitarra.precio }}</p>
                    <button 
                        @click="$emit('agregar-carrito')"

                        type="button"
                        class="btn btn-dark w-100 "
                    >Agregar al Carrito</button>
                                            <!-- Aqui emitimos el evento con emit() -->
                </div>
            </div><!-- FIN GUITARRA -->
</template>