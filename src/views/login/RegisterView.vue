<template>
    <br>
    <nav class="navbar  bg-light container rounded-4">
        <div class="container-fluid">
            <ol class="breadcrumb">
                <li class="breadcrumb-item"><a href="/">Home</a></li>
                <li class="breadcrumb-item active" aria-current="page"><a href="/Books">User</a></li>
                <li class="breadcrumb-item active" aria-current="page">New User</li>
            </ol>
            <div class="d-flex">

            </div>
        </div>

    </nav>

    <br>


    <div class="container">
        <form class="row g-3" action="/api/useradd" method="POST" @submit.prevent="save">
            <div class="col-md-6">
                <label for="exampleInputEmail1" class="form-label" style="float:left">Email address</label>
                <input type="email" class="form-control" v-model="user.email" aria-describedby="emailHelp">
            </div>
            <div class="col-md-6">
                <label for="exampleInputPassword1" class="form-label" style="float:left">Full Name</label>
                <input type="text" class="form-control" v-model="user.fullname">
            </div>
            <div class="col-md-4">
                <label for="exampleInputPassword1" class="form-label" style="float:left">Password</label>
                <input type="password" class="form-control" v-model="user.password">
            </div>
            <div class="col-md-4">
                <label for="exampleInputPassword1" class="form-label" style="float:left">Type</label>
                <select id="inputState" class="form-select" v-model="user.type">
                    <option selected>Open this select menu...</option>
                    <option>...</option>
                </select>
            </div>
            <div class="col-md-4">
                <label for="exampleInputPassword1" class="form-label" style="float:left">Phone</label>
                <input type="text" class="form-control" v-model="user.phone">
            </div>

            <div>
                <button type="submit" class="btn btn-primary" style="float:left">Save</button>
            </div>
        </form>
    </div>
</template>
  
<script>
import { ref } from "vue";

export default {
    name: 'RegisterView',
    setup() {
        const user = ref({});

        const save = async function () {
            var response = await fetch("/api/useradd", {
                method: "post",
                headers: {
                    // 'Content-Type': 'application/x-www-form-urlencoded',
                    'Content-Type': 'application/json'
                },

                // body: new URLSearchParams(new FormData(event.target))
                body: JSON.stringify(user.value)
            });
            alert("create an account.")
            console.log(response)


        }

        return {
            user, save
        }

        }

    }
</script>
