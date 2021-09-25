<template>
    <div id="login">
        <input type="email" v-model="email" />
        <input type="password" v-model="password">
        <button @click="googleSignIn">Google sign in</button>

        
    </div>
</template>
<script>
//import firebase from "firebase";
export default {
    data(){
        return{
            email:"",
            password:"",
        };
    },
    methods:{
        googleSignIn: function(){
            const provider = new firebase.auth.GoogleAuthProvider();
            firebase.suth().signInWithPopup(provider).then(() =>{
                alert("Sign in!");
            }).catch(err =>{
                console.log(err);
            });
        },
    },
};
</script>
