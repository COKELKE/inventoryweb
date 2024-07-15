<template>
    <br>
    <div class="container">
        <form @submit.prevent="login()">
            <div class="mb-3">
                <label for="exampleInputEmail1" style="float:left" class="form-label">Email address</label>
                <input type="email" class="form-control" v-model="credential.email" aria-describedby="emailHelp">
                <div id="emailHelp" style="float:left" class="form-text">We'll never share your email with anyone else.</div>
            </div>
            <br>
            <div class="mb-3">
                <label for="exampleInputPassword1" style="float:left" class="form-label">Password</label>
                <input type="password" class="form-control" v-model="credential.password">
            </div>
            <div class="mb-3 form-check">
                <input type="checkbox" class="form-check-input">
                <label class="form-check-label" style="float:left" for="exampleCheck1">Check me out</label>
            </div>
            <router-link :to="`/home`"><button class="btn btn-primary" style="float:left" type="submit">Submit</button></router-link>
        </form>
    </div>
</template>
  
<script>
import { ref } from "vue";
import jwt_decode from "jwt-decode";

export default {
    name: 'LoginView',
    setup() {
        const credential = ref({});

        const login = async function () {

            var response = await fetch("/api/login", {
                method: "post",
                headers: {
                    "content-type": "application/json"
                },
                body: JSON.stringify(credential.value)
            });

            if (response.ok) {
                var data = await response.json()
                localStorage.setItem("user", data.token);

                var decoded = jwt_decode(data.token);
                alert(JSON.stringify(decoded))

                // alert(JSON.stringify(data))
                alert("login Successfully.")

            } else {
                alert(response.statusText)
            }
        }

        return {
            credential, login
        }
    }
}
</script>