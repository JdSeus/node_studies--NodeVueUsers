<template>
    <div>
        <br>
        <br>
        <h2>Edição de usuário!</h2>
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

                <hr>
                <button @click="update" class="button is-success">Editar</button>
            </div>
        </div>  
    </div>
</template>

<script>
import axios from 'axios'
export default {
    created() {
        var req = {
            headers: {
                Authorization: "Bearer " + localStorage.getItem('token')
            }
        }

        axios.get("http://localhost:8686/user/" + this.$route.params.id, req).then(res => {
            console.log(res);

            this.name = res.data.name;
            this.email = res.data.email;
            this.id = res.data.id;

        }).catch(err => {
            console.log(err);
            this.$router.push({name: 'Users'});
        });
    },
    data(){
        return {
            name: '',
            email: '',
            id: -1,
            error: undefined,
        }
    },
    methods: {
        update(){
            axios.put("http://localhost:8686/user",{
                name: this.name,
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