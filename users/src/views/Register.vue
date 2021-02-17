<template>
    <div>
        <br>
        <br>
        <h2>Registro de usuário!</h2>
        <hr>
        <div class="columns is-centered">
            <div class="column is-half">
                <div v-if="error != undefined">
                    <hr>
                    <div class="notification is-danger">
                        <p>{{error}}</p>
                    </div>
                    <hr>
                </div>
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
            email: '',
            error: undefined
        }
    },
    methods: {
        register(){
            axios.post("http://localhost:8686/user",{
                name: this.name,
                password: this.password,
                email: this.email
            }).then((res) => {
                console.log(res);
                this.$router.push({name: 'Home'});
            }).catch((err) => {
                if (err.response.data.err != undefined) {
                    this.error = err.response.data.err;
                }
            });

        }
    }
}
</script>

<style scoped>
</style>