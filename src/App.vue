<script setup>
    import { ref, reactive, onMounted } from 'vue'
    import { db } from './data/guitarras.js'

    // Componentes
    import CardGuitar from './components/CardGuitar.vue'
    import Header from './components/Header.vue'

    const guitarras = ref([])
    const carrito = ref([])

    onMounted(() => {
        guitarras.value = db;
    })
    
    const agregarCarrito = (guitarra) => {
        guitarra.cantidad = 1;
        carrito.value.push(guitarra);
    }

</script>

<template>
    <Header/>
    <main class="container-xl mt-5">
        <h2 class="text-center">Nuestra Colección</h2>

        <div class="row mt-5">
            <CardGuitar
                v-for="guitarra in guitarras"
                :guitarra="guitarra"
                @agregar-carrito="agregarCarrito"
            />
        </div>
    </main>


    <footer class="bg-dark mt-5 py-5">
        <div class="container-xl">
            <p class="text-white text-center fs-4 mt-4 m-md-0">GuitarLA - Todos los derechos Reservados</p>
        </div>
    </footer>
</template>

<style scoped>
</style>
