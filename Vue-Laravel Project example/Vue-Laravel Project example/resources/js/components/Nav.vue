<template>
<nav>

    <div class="navbar-main" @click="ToggleNavbar">

        <p class="nav_title_text">Menu</p>
        
    </div>

    <div class="links">
        <div v-if="navbar" class="links_holder">
            <router-link class="route_link gradient_text" to="/pebblin" @click="ToggleNavbar">Add Pebblin</router-link>

            <div class="links_spacer"></div>

            <router-link class="route_link" to="/" @click="ToggleNavbar">Home</router-link>

            <div class="links_spacer"></div>

            <router-link class="route_link" to="/profile" @click="ToggleNavbar">Profile</router-link>

            <div class="links_spacer"></div>

            <router-link class="route_link" to="/" @click="ToggleNavbar">Settings</router-link>

            <div class="links_spacer"></div>

            <span class="route_link" @click="ToggleNavbar(); toggleModal('login');">Login</span>

             <div class="links_spacer"></div>

            <span class="route_link" @click="ToggleNavbar(); toggleModal('signup');">Signup</span>

            <div class="links_spacer"></div>

            <router-link class="route_link danger_text" to="/" @click="ToggleNavbar">Logout</router-link>
        </div>
    </div>

    
</nav>

<div v-if="showModal">
    <Modal @close="closeModals">
        <div v-if="loginModal">
            <Login_comp></Login_comp>
        </div>

        <div v-if="signupModal">
            <Signup_comp></Signup_comp>
        </div>
    </Modal>
</div>
</template>

<script>
import Modal from './Modal.vue'
import Login_comp from './login/Login_comp.vue'
import Signup_comp from './login/Signup.vue'

export default {
    components: { Modal, Login_comp, Signup_comp },

    data() {
        return {
            navbar: false,
            navbarHeightHolder: '',
            showModal: false,
            loginModal: false,
            signupModal: false,
            LoginStatus: false
        }
    },

    created() {
        LoginStatus = this.$watch(sessionStorage.getItem('loggedIn'))
    },

    methods: {
        ToggleNavbar() {
            this.navbar = !this.navbar

            // 44 is the height of the nav element
            const height = $(window).height() - 44;

            if  (this.navbar) {

                $(".navbar-main").css("top", height);

                 $('.navbar-main').stop().animate({
                     top: 0
                 }, 500, function() {

                });

                $('.links').stop().animate({
                     height: '100%'
                 }, 500, function() {

                });

            } else {

                $('.navbar-main').stop().animate({
                     top: height
                 }, 500, function() {
                     $(".navbar-main").css("top", '');
                });

                $('.links').stop().animate({
                     height: '0%'
                 }, 500, function() {

                });
            }


                // if (this.navbar) {

                //     const height = document.querySelector('.navbar-main').offsetHeight

                //     this.navbarHeightHolder = height

                //     $('.navbar-main').stop().animate({
                //     height: "100%"
                //     }, 500, function() {

                //     });
                // } else {
                //     $('.navbar-main').stop().animate({
                //     height: this.navbarHeightHolder
                //     }, 500, function() {

                //     });
                // }


            },

        toggleModal(type) {

            if (type == 'login') {
                this.showModal = !this.showModal
                this.loginModal = !this.loginModal
            } else if (type == 'signup') {
                this.showModal = !this.showModal
                this.signupModal = !this.signupModal
            }
        },

        closeModals() {
        if (this.showModal) {
            this.showModal = !this.showModal
            this.signupModal = false
            this.loginModal = false
        }
        },

        testLoginSession() {
            console.log(this.LoginStatus)
        }
    }

}

</script>

<style>
    .navbar-main {
        width: 100%;
        height: 55px;
        position: fixed;
        bottom: 0;
        border: 1px solid #d5d5d5;
        z-index: 2000;
        background: rgb(231,232,233);
        background: -moz-linear-gradient(0deg, rgba(215,215,215,1) 0%, rgba(255,255,255,1) 100%);
        background: -webkit-linear-gradient(0deg, rgba(215,215,215,1) 0%, rgba(255,255,255,1) 100%);
        background: linear-gradient(0deg, rgba(215,215,215,1) 0%, rgba(255,255,255,1) 100%);
        filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#e7e8e9",endColorstr="#ffffff",GradientType=1);
        -webkit-box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.12);
        -moz-box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.12);
        box-shadow: 0px 0px 5px 0px rgba(0,0,0,0.12);
    }

nav {
    text-align: center;
}


nav a {
    font-weight: bold;
    color: #2c3e50;
    font-size: 30px;
    text-decoration: none;
}

.route_link {
    text-decoration: none;
    font-family: 'Maven Pro', sans-serif;
    font-weight: 500;
    font-size: 20px;
    color: #949699;
    padding: 15px;
}

.gradient_text {
    background: rgb(254,0,1);
    background: -moz-linear-gradient(90deg, rgba(254,0,1,1) 0%, rgba(90,111,253,1) 100%);
    background: -webkit-linear-gradient(90deg, rgba(254,0,1,1) 0%, rgba(90,111,253,1) 100%);
    background: linear-gradient(90deg, rgba(254,0,1,1) 0%, rgba(90,111,253,1) 100%);
    filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#fe0001",endColorstr="#5a6ffd",GradientType=1);
    background-clip: text;
    color: transparent
}

.danger_text {
    color: #F05050;
}

.links_holder {
    text-align: center;
    padding-top: 30px;
    
}

.links_spacer {
    height: 1px;
    background: rgb(255,255,255);
    background: -moz-linear-gradient(135deg, rgba(255,255,255,0) 0%, rgba(186,188,190,1) 40%, rgba(186,188,190,1) 60%, rgba(255,255,255,0) 100%);
    background: -webkit-linear-gradient(135deg, rgba(255,255,255,0) 0%, rgba(186,188,190,1) 40%, rgba(186,188,190,1) 60%, rgba(255,255,255,0) 100%);
    background: linear-gradient(135deg, rgba(255,255,255,0) 0%, rgba(186,188,190,1) 40%, rgba(186,188,190,1) 60%, rgba(255,255,255,0) 100%);
    filter: progid:DXImageTransform.Microsoft.gradient(startColorstr="#ffffff",endColorstr="#ffffff",GradientType=1);
}

.links {
    line-height: 80px;
    padding-top: 20px;
    background-color: #f5f5f5;
    z-index: 1999;
    height: 0%;
    width: 100%;
    bottom: 0;
    position: fixed;
}

.nav_title_text {
   margin-top: 13px;
    font-size: 22px;
    font-weight: 500;
    color: #00000073;
}


</style>