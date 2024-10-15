<template>
    <div class="container mt-4 d-flex flex-column align-items-center">
        <div class="d-flex flex-column align-items-center border border-solid rounded-4 p-5">
            <div class="d-flex flex-row justify-content-center text-center">
                <div class="mb-4 me-2" style="flex: 3">
                    <label :class="{ 'text-danger': !cita.paciente }" class="fw-bold" for="paciente">Paciente</label>
                    <input type="text" class="form-control mt-2" v-model="cita.paciente" id="paciente">
                </div>
                <div class="mb-3 me-2" style="flex: 1">
                    <label :class="{ 'text-danger': !cita.fecha }" class="fw-bold" for="fecha">Fecha</label>
                    <input type="date" class="form-control mt-2" v-model="cita.fecha" id="fecha">
                </div>
                <div class="mb-3 me-2" style="flex: 1">
                    <label :class="{ 'text-danger': !cita.hora }" class="fw-bold" for="hora">Hora</label>
                    <input type="time" class="form-control mt-2" v-model="cita.hora" id="hora">
                </div>
                <div class="mb-3 me-2" style="flex: 2">
                    <label :class="{ 'text-danger': !cita.gravedad }" class="fw-bold" for="gravedad">Gravedad</label>
                    <select class="form-select mt-2" v-model="cita.gravedad" id="gravedad">
                        <option disabled value="">Selecciona</option>
                        <option value="Baja">Baja</option>
                        <option value="Media">Media</option>
                        <option value="Alta">Alta</option>
                    </select>
                </div>
                <div class="mb-3" style="flex: 3">
                    <label :class="{ 'text-danger': !cita.motivo }" class="fw-bold" for="motivo">Motivo</label>
                    <input type="text" class="form-control mt-2" v-model="cita.motivo" id="motivo">
                </div>
            </div>
            <button type="submit" class="btn btn-primary" :disabled="!formularioCompleto">Agregar</button>
        </div>

        <p v-if="citas.length === 0" class="mt-5">Aún no hay consultas registradas.</p>

        <div v-else class="mt-3 d-flex flex-wrap justify-content-center text-center">
            <CitaCard v-for="(cita, index) in citas" :key="index" :cita="cita" @eliminar="eliminarCita(index)" />
        </div>
    </div>
</template>

<script>
import CitaCard from './CitaCard.vue';

export default {
    data() {
        return {
            cita: {
                paciente: '',
                fecha: '',
                hora: '',
                gravedad: '',
                motivo: ''
            },
            citas: []
        };
    },
    computed: {
        formularioCompleto() {
            return this.cita.paciente && this.cita.fecha && this.cita.hora && this.cita.gravedad && this.cita.motivo;
        }
    },
    methods: {
        agregarCita() {
            this.citas.push({ ...this.cita });
            this.cita = { paciente: '', fecha: '', hora: '', gravedad: '', motivo: '' };
        },
        eliminarCita(index) {
            this.citas.splice(index, 1);
        }
    },
    components: {
        CitaCard
    }
};
</script>