<script setup>
  import { ref, reactive } from 'vue'
  import { uid } from 'uid'

  import Header from './components/Header.vue'
  import Formulario from './components/Formulario.vue'
  import Paciente from './components/Paciente.vue'

  var pacientes = ref([])

  const paciente = reactive({
    id: null,
    nombre: '',
    propietario: '',
    email: '',
    alta: '',
    sintomas: ''
  })

  const guardarPaciente = () => {
    if(paciente.id){
      const { id } = paciente;
      //retornar la posición del paciente en el arreglo
      const i = pacientes.value.findIndex((pacienteState) => pacienteState.id === id)
      // actualizar el arreglo de pacientes
      pacientes.value[i] = {...paciente}
    }
    else{
      pacientes.value.push({
        ...paciente, 
        id: uid() // generar un id único
      })
    }

    // limpiar el formulario
    Object.assign(paciente, {
      nombre: '',
      propietario: '',
      email: '',
      alta: '',
      sintomas: '',
      id: null
    })
  }

  const actualizarPaciente = (id) => {
    const pacienteEditar = pacientes.value.filter(paciente => paciente.id === id)[0]
    Object.assign(paciente, pacienteEditar)
  }

</script>

<template>
  <div class="container mx-auto mt-20">
    <Header/>

    <div class="mt-12 md:flex">
      <Formulario
        v-model:nombre="paciente.nombre"
        v-model:propietario="paciente.propietario"
        v-model:email="paciente.email"
        v-model:alta="paciente.alta"
        v-model:sintomas="paciente.sintomas"
        @guardar-paciente="guardarPaciente"
      />

      <!-- listado de pacientes del formulario -->
      <div class="md:w-1/2 md:h-screen overflow-y-scroll">
        <h3 class="font-black text-3xl text-center"> Administra tus pacientes</h3>

        <div v-if="pacientes.length > 0">

          <p class="text-lg text-center mt-5 mb-10">
            Información de 
            <span class="text-indigo-600 font-bold">Pacientes</span> 
          </p>

          <Paciente
            v-for="paciente in pacientes"
            :key="paciente.id"
            :paciente="paciente"
            @actualizar-paciente="actualizarPaciente"
          />

        </div>
        <p v-else class="mt-10 text-2xl text-center">
          No hay pacientes
        </p>

      </div>

    </div>

  </div>
</template>