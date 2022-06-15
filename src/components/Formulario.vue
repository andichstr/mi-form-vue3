<template>
    <div class="container">
        <form class="form" action="">
            <div class="row">
                <div class="col-3">
                    <label for="username">Nombre y apellido: </label>
                </div>
                <div class="col-9">
                    <input type="text" id="username" placeholder="Tu nombre y apellido" class="form-control" @keyup="validateNombre" v-model="usuario.nombre"/>
                </div>
            </div>
            <div class="row" v-if='validNombre != ""'>
                <p class="errorForm">{{ validNombre }}</p>
            </div>
            <div class="row">
                <div class="col-3">
                    <label for="username">Mail: </label>
                </div>
                <div class="col-9">
                    <input type="text" id="email" placeholder="Tu email" class="form-control" @keyup="validateEmail" v-model="usuario.email"/>
                </div>
            </div>
            <div class="row" v-if='validMail != ""'>
                <p class="errorForm">{{ validMail }}</p>
            </div>
            <div class="row">
                <div class="col-3">
                    <label for="username">Edad: </label>
                </div>
                <div class="col-9">
                    <input type="number" id="edad" placeholder="Tu edad" class="form-control" @keyup="validateEdad" v-model="usuario.edad"/>
                </div>
            </div>
            <div class="row" v-if='validEdad != ""'>
                <p class="errorForm">{{ validEdad }}</p>
            </div>
            <div class="row">
                <div class="col-3">
                    <label for="password">Contraseña: </label>
                </div>
                <div class="col-9">
                    <input type="password" id="password" placeholder="Tu contraseña" class="form-control" @keyup="validatePassword" v-model="usuario.password"/>
                </div>
            </div>
            <div class="row" v-if='validPassword != ""'>
                <p class="errorForm">{{ validPassword }}</p>
            </div>
            <div class="row">
                <input type="button" class="btn btn-agregar" value="Agregar" @click="agregarUsuario"/>
            </div>
        </form>
    </div>
</template>

<script>
import { ref } from '@vue/reactivity'
export default {
    setup() {
        const usuario = ref({
                nombre: "",
                password: "",
                email: "",
                edad: "",
            });
            const validNombre = ref("");
            const validPassword = ref("");
            const validMail = ref("");
            const validEdad = ref("");
        return {
            usuario, validNombre, validPassword, validMail, validEdad
        }
    },
    methods: {
        agregarUsuario() {
            if (this.checkForm()){
                this.$emit('agregar-usuario-tabla', this.usuario);
                this.usuario.nombre = "";
                this.usuario.password = "";
                this.usuario.email = "";
                this.usuario.edad = "";
            } else {
                alert("Por favor, corrija los errores del formulario y vuelva a intentarlo");
            }
        },
        checkForm () {
            return (this.validateNombre() && this.validateEmail() && this.validateEdad() && this.validatePassword())
            },
        validateNombre(){
            let reg_ex_nombre = /[a-zA-Z]{2,}\s[a-zA-Z]{2,}/g;
            if (reg_ex_nombre.test(this.usuario.nombre)){
                this.validNombre = "";
                return true;
            } else {
                this.validNombre = "Debe escribir su nombre y apellido, y deben contener al menos dos letras cada uno.";
                return false;
            }
        },
        validateEmail(){
            let reg_ex_mail = /^[^@]+@[^@]+.[a-zA-Z]{2,}$/;
            if (reg_ex_mail.test(this.usuario.email)){
                this.validMail = "";
                return true;
            } else {
                this.validMail = "Mail inválido";
                return false;
            }
        },
        validateEdad(){
            if (this.usuario.edad >= 18 && this.usuario.edad <= 100){
                this.validEdad = "";
                return true;
            } else {
                this.validEdad = "Debe ingresar una edad entre 18 y 100 años.";
                return false;
            }
        },
        validatePassword(){
            let reg_ex_password = /^(?=.*?[A-Z])(?=.*?[a-z])(?=.*?[0-9])(?=.*?[#?!@$%^&*-]).{8,}$/;
            if (reg_ex_password.test(this.usuario.password)){
                this.validPassword = "";
                return true;
            } else {
                this.validPassword = "La contraseña debe contener al menos 8 caracteres, una mayúscula, un caracter especial y un número."
                return false;
            }
        }
    }
}
</script>

<style scoped>

    input{
        width: 100%;
    }

    .col-3{
        text-align: right;
    }

    .form{
        border: 1px solid #88B6CB;
        padding-left: 20px;
        padding-right: 20px;
        padding-top: 10px;
        padding-bottom: 10px;
    }

    .errorForm{
        color: red;
        font-size: small;
    }

    .btn-agregar{
        background-color: #88B6CB;
    }

</style>