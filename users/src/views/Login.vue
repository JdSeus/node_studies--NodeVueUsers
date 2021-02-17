<template>
    <div>
        <br>
        <br>
        <h2>Login</h2>
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

                <p>E-mail</p>
                <input v-model="email" class="input" type="email" placeholder="email@email.com">

                <p>Senha</p>
                <input v-model="password" class="input" type="password" placeholder="********">

                <hr>
                <button @click="login" class="button is-success">Logar</button>
            </div>
        </div>  
    </div>
</template>

<script>
import axios from 'axios'
export default {
    data(){
        return {
            password: '',
            email: '',
            error: undefined,
        }
    },
    methods: {
        login(){
             axios.post("http://localhost:8686/login",{
                password: this.password,
                email: this.email
            }).then((res) => {
                console.log(res);
                localStorage.setItem('token', res.data.token);
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