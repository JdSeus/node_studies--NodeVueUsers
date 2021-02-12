<template>
    <div>
        <br>
        <br>
        <h2>Registro de usuário!</h2>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <p>Nome</p>
                <input v-model="name" class="input" type="text" placeholder="Nome do usuário">

                <p>E-mail</p>
                <input v-model="email" class="input" type="email" placeholder="email@email.com">

                <p>Senha</p>
                <input v-model="password" class="input" type="password" placeholder="********">

                <hr>
                <button @click="register" class="button is-success">Cadastrar</button>
            </div>
        </div>  
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return {
            name: '',
            password: '',
            email: ''
        }
    },
    methods: {
        register(){
            axios.post("http://localhost:8686/user",{
                name: this.name,
                password: this.password,
                email: this.email
            }).then(res => {
                console.log(res);
            }).catch(err => {
                var msgErro = err.response.data.err
                console.log(msgErro);
            });

        }
    }
}
</script>

<style scoped>
</style>