<template>
    <section class="edit border border-primary rounded">
        <div>
            <form>
                <h3 class="text-secondary">Editar persona</h3>
                <div class="form-group">
                    <label for="exampleInputEmail1">{{ msg.number_identification }}</label>
                    <input type="text" class="form-control mb-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Numero de indentificación" v-model="number_identification">
                    <label for="exampleInputEmail1">{{ msg.full_name }}</label>
                    <input type="text" class="form-control mb-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Nombres" v-model="full_name">
                    <label for="exampleInputEmail1">{{ msg.full_last_name }}</label>
                    <input type="text" class="form-control mb-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Apellidos" v-model="full_last_name">
                    <label for="exampleInputEmail1">{{ msg.birthdate }}</label>
                    <input type="text" class="form-control mb-3" id="exampleInputEmail1" aria-describedby="emailHelp" placeholder="Cumpleaños" v-model="birthdate">
                    <label for="exampleInputEmail1">{{ msg.sex }}</label>
                    <div class="mb-3 ms-2 me-2">
                        <select class="custom-select text-secondary border border-info rounded pb-1 pt-1 sform" v-model="sex">
                            <option value="m">Masculino</option>
                            <option value="f">Femenino</option>
                            <option value="init">Seleccione genero</option>
                        </select>
                    </div>
                </div>
                <button type="button" class="btn btn-primary" @click="addPeople">Editar</button>
            </form>
        </div>
    </section>
</template>

<style>
    @import url('./../static/css/editar.css');
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
        props: {
            msg: {}
        },
        methods: {
            addPeople(){
                let url = 'http://localhost:4000/updatePeople'
                axios.post(url,{
                    "data": {
                        "number_identification": this.msg.number_identification,
                        "full_name": this.full_name,
                        "full_last_name": this.full_last_name,
                        "birthdate": this.birthdate,
                        "sex": this.sex
                    }
                }).then( response => {
                    console.log(this.msg.number_identification)
                    this.$emit('operation', 'add')
                }).catch(e => console.log(e))
            }
        }
    }
</script>