<template>
    <section class="add border border-primary rounded">
        <div>
            <form>
                <h3 class="text-secondary">Agregar persona</h3>

                <div class="form-group">
                    <input type="text" class="form-control mt-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Numero de indentificación" v-model="number_identification">
                    <input type="text" class="form-control mt-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Nombres" v-model="full_name">
                    <input type="text" class="form-control mt-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Apellidos" v-model="full_last_name">
                    <input type="text" class="form-control mt-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Cumpleaños" v-model="birthdate">
                    
                    <div class="mt-3 ms-2 me-2">
                        <select class="custom-select text-secondary border border-info rounded pb-1 pt-1 sform" v-model="sex">
                            <option value="m">Masculino</option>
                            <option value="f">Femenino</option>
                            <option value="init">Seleccione genero</option>
                        </select>
                    </div>
                </div>
                <button type="submit" class="btn btn-primary" @click="addPeople">Agregar</button>
            </form>
        </div>
    </section>
</template>

<style>
    @import url('./../static/css/agregar.css');
</style>

<script>
    import axios from 'axios';
    export default {
        data() {
            return {
                number_identification: '',
                full_name: '',
                full_last_name: '',
                birthdate: '',
                sex: 'init'
            }
        },
        methods: {
            addPeople(){
                let url = 'http://localhost:4000/createPeople'
                axios.post(url,{
                    "data": {
                        "number_identification": this.number_identification,
                        "full_name": this.full_name,
                        "full_last_name": this.full_last_name,
                        "birthdate": this.birthdate,
                        "sex": this.sex
                    }
                }).then( response => {
                    console.log(response)
                    this.$emit('operation', 'add')
                }).catch(e => console.log(e))
            }
        }
    }
</script>