<template>
    <div class="container">    
        <h1 class="text-start">Carreras List
        <button @click="newCarrera()" class="btn btn-success mx-2">
            <font-awesome-icon icon="plus" />
        </button>
    </h1>
        <table class="table">
            <thead>
                <tr>
                    <th scope="col">#</th>
                    <th scope="col">Id</th>
                    <th scope="col">Nombre</th>
                    <th scope="col">Descripción</th>                        
                </tr>
            </thead>
            <tbody>       
                <tr v-for="(carrera, index) in carreras" :key="index">
                    <th scope="row">{{ index + 1 }}</th>
                    <td>{{ carrera.id }}</td>
                    <td>{{ carrera.nombre }}</td>
                    <td>{{ carrera.descripcion }}</td>  
                    <td>                    
                        <button @click="deleteCarrera(carrera.id)" class="btn btn-danger mx-2">
                            <font-awesome-icon icon="trash" />
                        </button> 
                        <button @click="editCarrera(carrera.id)" class="btn btn-warning mx-2">
                            <font-awesome-icon icon="pencil" />
                        </button> 
                    </td>                                         
                </tr>       
            </tbody>
        </table>
    </div>   
</template>

<script>
import axios from 'axios';
import Swal from 'sweetalert2';

export default {
    name: 'Carrera',
    data() {
        return {
            carreras: []
        };
    },
    methods: {
        deleteCarrera(id) {
            Swal.fire({
                title: `Do you want to delete the Carrera with id ${id}?`,
                showCancelButton: true,
                confirmButtonText: 'Delete',
            }).then((result) => {
                if (result.isConfirmed) {
                    axios.delete(`http://127.0.0.1:8000/api/carreras/${id}`)
                        .then(response => {
                            if (response.data.success) {
                                Swal.fire('Deleted!! ', '', 'success');
                                this.carreras = response.data.carreras;
                            }
                        });
                }
            });
        },
        editCarrera(id) {
            this.$router.push({ name: 'EditarCarrera', params: { id: `${id}` } });
        },
        newCarrera() {
            this.$router.push({ name: 'NewCarrera' });
        },
    },
    mounted() {
        axios
            .get('http://127.0.0.1:8000/api/carreras')
            .then(response => (this.carreras = response.data.carreras.data));
    },
};
</script>
