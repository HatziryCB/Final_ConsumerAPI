<script>
import axios from 'axios';

export default {
    name: 'ComponenteExamenFinal',
    data() {
        return {
            picsumData: [], //Array para las imagenes
        };
    },
    mounted() {
        this.fetchPicsumData();
    },
    methods: {
        async fetchPicsumData() {
            try {
                const response = await axios.get('https://picsum.photos/v2/list');
                this.picsumData = response.data;
            } catch (error) {
                console.error('Error al obtener datos de la API:', error);
            }
        }
    }
};
</script>

<template>
    <div class="container-sm">
        <h2 class="text-center mt-4" style="background: linear-gradient(to bottom right, #000, #434343); color: #fff;">
            Lista de imágenes de Picsum
        </h2>

        <div v-if="picsumData.length" class="row">
            <div v-for="image in picsumData" :key="image.id" class="col-md-4">
                <div class="card mt-3">
                    <img :src="image.download_url" class="card-img-top" :alt="`Imagen de ${image.author}`" />
                    <div class="card-body">
                        <h5 class="card-title">{{ image.author }}</h5>
                        <a :href="image.download_url" target="_blank" class="btn btn-primary">Descargar imagen</a>
                    </div>
                </div>
            </div>
        </div>

        <div v-else>
            <p>Cargando imágenes...</p>
        </div>
    </div>
</template>

<style scoped>
.text-center {
    text-align: center;
}
.card {
    margin: auto;
    max-width: 100%;
}
.card-img-top {
    max-width: 100%;
    height: auto;
}
</style>
