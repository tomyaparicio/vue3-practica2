<template>
  <section>
    <h3>Añadir Profesor</h3>

    <div>
      <label>Nombre:</label>
       <input type="text" v-model="teacher.teacherName" />
    </div>
    <div>
      <label>Apellido:</label>
       <input type="text" v-model="teacher.surname" />
    </div>
    <div>
      <label>DNI:</label>
       <input type="text" v-model="teacher.dni" />
    </div>
    <div>
      <label>Materias</label> 
      <input placeholder="Añadir Materia" type="text" v-model="subject" />
      <button @click="handleSubject()">Añadir</button>
    </div>
    <div>
      <ul>
      <li v-for="(materia, index) in teacher.subjects" :key="index">
        {{ materia }}
      </li>
    </ul>
    </div>
    <input type="checkbox" v-model="teacher.doc"/> Documentacion Entregada
    <button @click="handleTeacher()">Agregar</button>
  </section>
  <section>
    <h3>Listado De Profesores</h3>
   <table>
    <tr>
      <th>Nombre</th>
      <th>Apellidos</th>
      <th>Dni</th>
      <th>Materias</th>
      <th>Documentacion Entregada</th>
    </tr>
    <tr v-for="profesor in teachers" :key="profesor.dni">
      <th>{{ profesor.teacherName }}</th>
      <th>{{ profesor.surname }}</th>
      <th>{{ profesor.dni }}</th>
      <th>
        <ul>
          <li v-for="(item, index) in profesor.subjects" :key="index" >
            {{ item }}
          </li>
        </ul> 
      </th>
      <th v-if="profesor.doc = true">
        Entregado
      </th>
      <th v-else>
        Entregado
      </th>
    </tr>
   </table>
  </section>
</template>

<script lang="ts" setup>
import {ref, Ref} from 'vue'

interface ITeacher{
  teacherName: string,
  surname: string,
  dni: string,
  subjects: Array<string>,
  doc: boolean, 
}

let teacher:Ref<ITeacher> = ref({
          teacherName: '',
          surname:'',
          dni: '',
          subjects: [],
          doc: false,
})

let teachers:Ref<Array<ITeacher>> = ref([])

let subject:Ref<string> = ref('')

const handleSubject = () =>{
  teacher.value.subjects.push(subject.value)
  subject.value = ""
}

const handleTeacher = () =>{
    teachers.value.push({
      teacherName: teacher.value.teacherName,
      surname: teacher.value.surname,
      dni: teacher.value.dni,
      subjects:  teacher.value.subjects,
      doc:  teacher.value.doc,
    })
    teacher.value.teacherName = ''
    teacher.value.surname = ''
    teacher.value.dni = ''
    teacher.value.subjects = []
    teacher.value.doc = false
}
</script>

<style scoped>

</style>
