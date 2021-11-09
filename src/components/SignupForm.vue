<template>
    <form id="signup-form" @submit="postData" method="POST">
        <div class="row">
            <div class="col-12 form-group">
                <label class="col-form-label col-form-label-lg">Nome <span class="text-danger">*</span></label>
                <input type="text" v-model="nome" class="form-control form-control-lg">
            </div>
            <div class="col-12 form-group">
                <label class="col-form-label col-form-label-lg">Cognome <span class="text-danger">*</span></label>
                <input type="text" v-model="cognome" class="form-control form-control-lg">
            </div>
            <div class="col-12 form-group">
                <label class="col-form-label col-form-label-lg">Email <span class="text-danger">*</span></label>
                <input type="text" v-model="$v.email.$model" :class="{'is-invalid': validationStatus($v.email)}" class="form-control form-control-lg">
                <div v-if="!$v.email.required.email" class="invalid-feedback">Inserire email corretta.</div>
            </div>
            <div class="col-12 form-group text-center padtop2">
                <button type="submit" class="btn btn-vue btn-lg col-4 ">Registra</button>
            </div>
        </div>
    </form>
</template>

<script>
/* 
import axios from 'axios'
import * as Vue from 'vue'
import App from './App.vue'
import VueAxios from 'vue-axios'
import { createApp } from 'vue'
// import AppVue from '../App.vue'

const app = Vue.createApp(...)
app.use(VueAxios, axios) */

import {required, email} from 'vuelidate/lib/validators'

export default {
    name: 'SignupForm',
    data: function(){
        return {
                nome: '',
                cognome: '',
                email: '' 
        }
    },
    validations: {
        email: {required, email}
    },

    mounted () {
    },

    methods: {


        validationStatus: function(validation) {
            return typeof validation != "undefined" ? validation.$error : false;
        },

        

        postData(){
            this.axios.post("http://esempio.it", this.posts)
            .then((dati)=>{
                console.log(dati)
            }
            )


        }
    }
}
</script>
<style scoped>
.btn-vue{
    background-color: #42b983;
    margin-top: 20px;
    font-weight: bold;
}

</style>
