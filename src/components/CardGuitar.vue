<script setup>
import { ref, reactive, onMounted } from 'vue'
import { ContentLoader } from 'vue-content-loader';

const numero = ref(0)

const props = defineProps({
    guitarra: {
        type: Object,
        required: false, // Permitimos que sea null mientras carga
    }
});

defineEmits(['agregar-carrito'])

const loading = ref(true);

setTimeout(() => {
    loading.value = false;
}, 2000);
</script>

<template>
    <div class="col-md-6 col-lg-4 my-4 ms-2 row align-items-center">
        <template v-if="loading">
            <!-- Skeleton loader utilizando Vue Content Loader -->
            <ContentLoader :width="400" :height="150">
                <rect x="10" y="10" rx="5" ry="5" width="120" height="120" /> <!-- Imagen -->
                <rect x="140" y="10" rx="5" ry="5" width="250" height="20" /> <!-- Nombre -->
                <rect x="140" y="40" rx="5" ry="5" width="200" height="15" /> <!-- Descripción -->
                <rect x="140" y="70" rx="5" ry="5" width="150" height="20" /> <!-- Precio -->
                <rect x="140" y="100" rx="5" ry="5" width="200" height="30" /> <!-- Botón -->
            </ContentLoader>
        </template>
        <!-- Contenido real -->
        <template v-else>
            <div class="col-4">
                <img 
                    class="img-fluid" 
                    :src="'/img/' + guitarra.imagen + '.jpg'" 
                    :alt="'imagen guitarra ' + guitarra.nombre" 
                />
            </div>
            <div class="col-8">
                <h3 class="text-black fs-4 fw-bold text-uppercase">{{ guitarra.nombre }}</h3>
                <p>{{ numero }}</p>
                <p>{{ guitarra.descripcion }}</p>
                <p class="fw-black text-primary fs-3">${{ guitarra.precio }}</p>
                <button 
                    type="button" 
                    class="btn btn-dark w-100"
                    @click="$emit('agregar-carrito')"
                >Agregar al Carrito</button>
            </div>
        </template>
    </div>
</template>
