<template>

   <form @submit.prevent="handleLogin()">
     <div style="padding: 35px 0;">
                <h2 class="login_title" style="font-family: 'Maven Pro', sans-serif;">Login</h2>
    </div>

    <div class="email_container_login login">
        <input type="email" required v-model="formData.email" placeholder="Email:">
    </div>
  
    <div class="password_container_login login">
        <input type="password" required v-model="formData.password" placeholder="Password:">
    </div>

    <div class="button_container_login login">
        <button class="CTA_button_default">Login!</button>
    </div>
  </form>

    <button @click="getPosts">Posts</button>
    <button @click="logout">Farvel</button>

</template>

<script>
import axios from 'axios'
export default {
    data() {
        return {
            formData: {
                email: '',
                password: ''
            }
        }
    },

    methods: {
        handleLogin() {
            axios.get('/sanctum/csrf-cookie').then(response => {
                axios.post('/login',this.formData).then(response => {
                    console.log(response)
                    if (response.data.resp == "success") {
                        sessionStorage.setItem("loggedIn", "true");
                        this.$parent.closeModal();
                    } 
                })
            })
        },
        getPosts() {
            axios.get('/sanctum/csrf-cookie').then(response => {
                axios.get('api/posts',this.formData).then(response => {
                    console.log(response)
                })
            })
        },
        logout() {
            console.log(sessionStorage.getItem("loggedIn"));
            axios.get('/sanctum/csrf-cookie').then(response => {
                axios.post('/logout',this.formData).then(response => {
                    console.log(response)
                     if (response.data.resp == "success") {
                        console.log('Logged out')
                        this.$parent.closeModal()
                        
                    } 
                })
            })
        }
    }
}
</script>

<style>

.login_title {
    font-family: "Maven Pro", sans-serif;
    text-align: center;
    font-size: 43px;
    color: #ff6262;
    font-weight: 500;
    line-height: 30px;
    
}

.email_container_login {
    padding-bottom: 13px;
    display: flex;
    justify-content: center;

}

.password_container_login {
    padding-bottom: 26px;
    display: flex;
    justify-content: center;
}

.button_container_login {
    width: 85%;
    margin: auto;
    padding-bottom: 50px;
}

::placeholder { 
   color:    rgba(0,0,0,0.4);
   font-family: 'Maven Pro', sans-serif;
}

.login input {
    font-family: 'Maven Pro', sans-serif;
    padding: 9px;
    background: #f6fbff;
    width: 85%;
    border: none;
    font-size: 17px;
    -webkit-box-shadow: inset 0px 2px 10px 9px rgb(0 0 0 / 11%);
    -moz-box-shadow: inset 0px 2px 10px 9px rgba(0,0,0,0.11);
    box-shadow: inset 0px 1px 4px 0px rgb(0 0 0 / 25%);
    font-weight: 500;
}

</style>