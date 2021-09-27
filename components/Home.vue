<template>
  <section>
    <div class="header">
      <img src="./../static/horisoft.png" alt="">
      <h2 class="text-secondary">Test</h2>
      <button type="button" class="btn btn-primary-outline"><i class="fas fa-user-plus" @click="addPeople"></i></button>
    </div>

    <div class="home border border-primary rounded">
      <table class="table">
        <thead>
          <tr>
            <th scope="col">Identificación</th>
            <th scope="col">Nombre</th>
            <th scope="col">Apellido</th>
            <th scope="col">Fecha de nacimiento</th>
            <th scope="col">Sexo</th>
            <th scope="col">Acciones</th>
          </tr>
        </thead>
        <tbody>
          <tr v-for="datos in data" :key="datos.id_person">
            <th scope="row">{{ datos.number_identification}}</th>
            <td>{{ datos.full_name }}</td>
            <td>{{ datos.full_last_name }}</td>
            <td>{{ datos.birthdate }}</td>
            <td>{{ datos.sex}}</td>
            <td>
              <button class="btn btn-primary-outline"><i class="fas fa-edit" @click="editPeople(datos)"></i></button>
              <button class="btn btn-primary-outline"><i class="fas fa-trash-alt" @click="deletePeople(datos)"></i></button>
            </td>
          </tr>
        </tbody>
      </table>
    </div>
    
    <div>
      <agregar v-show="add == 'active'" @operation="addPeopleExit"></agregar>
      <editar v-show="edit == 'active'" :msg = "datos" @operation="addPeopleExit"></editar>
    </div>
  </section>
</template>

<style>
  @import url('./../static/css/home.css');
</style>

<script>
  import axios from 'axios';
  import VueRouter from 'vue-router'
  import Vue from 'vue'
  import agregar from './Agregar.vue'
  import editar from './Editar.vue'
  
  export default {
  data() {
    return {
      data: {},
      add: 'inactive',
      edit: 'inactive',
      dataEdit: '',
      datos: {}
    }
  },
  components:{
    agregar,
    editar
  },
  mounted(){
    let url = 'http://localhost:4000/getPeople'
    axios.get(url).then( response => {
      this.data = response.data.Data
    }).catch(e => console.log(e))
  },
  methods:{
    deletePeople(data){
      let url = 'http://localhost:4000/deletePeople'
      axios.post(url,{
        "data": {
          "number_identification": data.number_identification
        }
      }).then( response => {
        console.log(response)
      }).catch(e => console.log(e))
    },
    addPeople(){
      this.add = 'active'
    },
    addPeopleExit(){
      this.add = 'inactive'
      this.edit = 'inactive'
    },
    editPeople(data){
      this.edit = 'active'
      this.dataEdit = data
      this.datos = data
    }
  }
}
</script>
