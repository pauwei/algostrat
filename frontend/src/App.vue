<template>
    <div id="app">
        <h1>User Authentication</h1>
        <div>
            <h2>Register</h2>
            <input v-model="registerUsername" placeholder="Username" />
            <input v-model="registerPassword" placeholder="Password" type="password" />
            <button @click="register">Register</button>
        </div>
        <div>
            <h2>Login</h2>
            <input v-model="loginUsername" placeholder="Username" />
            <input v-model="loginPassword" placeholder="Password" type="password" />
            <button @click="login">Login</button>
        </div>
        <p v-if="message">{{ message }}</p>
    </div>
</template>

<script>
import axios from 'axios';

export default {
    data() {
        return {
            registerUsername: '',
            registerPassword: '',
            loginUsername: '',
            loginPassword: '',
            message: '',
        };
    },
    methods: {
        async register() {
            try {
                const response = await axios.post('http://localhost:5000/register', {
                    username: this.registerUsername,
                    password: this.registerPassword,
                });
                this.message = response.data;
            } catch (error) {
                this.message = 'Error registering user';
            }
        },
        async login() {
            try {
                const response = await axios.post('http://localhost:5000/login', {
                    username: this.loginUsername,
                    password: this.loginPassword,
                });
                this.message = `Login successful! Token: ${response.data.token}`;
            } catch (error) {
                this.message = 'Error logging in';
            }
        },
    },
};
</script>

<style>
#app {
    font-family: Avenir, Helvetica, Arial, sans-serif;
    text-align: center;
    margin-top: 50px;
}
input {
    margin: 5px;
}
</style>