<template>
  <br>
  <nav class="navbar  bg-light container rounded-4">
    <div>
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="/">Home</a></li>
        <li class="breadcrumb-item active" aria-current="page"><a href="/Games">Games</a></li>
        <li class="breadcrumb-item active" aria-current="page">Game Detail</li>
      </ol>
      <div class="d-flex">

      </div>
    </div>

  </nav>

  <br>
  <div class="container">
    <form class="row g-3" action="/api/inventoryDB" method="POST" @submit.prevent="save">
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Title</label>
        <input type="text" class="form-control" id="inputEmail4" name="gametitle" v-model="inventory.gametitle">
      </div>
      <div class="col-md-6">
        <label for="inputPassword4" class="form-label">Category</label>
        <select id="inputState" class="form-select" name="gamecategory" v-model="inventory.gamecategory">
          <option selected>Open this select menu...</option>
          <option>2D</option>
          <option>3D</option>
          <option>adult</option>
        </select>
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Image</label>
        <input type="text" class="form-control" id="inputCity" name="gameimage" v-model="inventory.gameimage">
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Publisher</label>
        <input type="text" class="form-control" id="inputCity" name="gamepublisher" v-model="inventory.gamepublisher">
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Quantity</label>
        <input type="text" class="form-control" id="inputCity" name="gamequantity" v-model="inventory.gamequantity">
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Location</label>
        <input type="text" class="form-control" id="inputCity" name="gamelocation" v-model="inventory.gamelocation">
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Description</label>
        <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" name="gamedescription"
          v-model="inventory.gamedescription"></textarea>
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Address</label>
        <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" name="gameaddress"
          v-model="inventory.gameaddress"></textarea>
      </div>
      <div>
        <button type="submit" class="btn btn-primary" style="float:left">Save</button>
        <button type="submit" class="btn btn-danger" style="float:right">Delete</button>
      </div>
    </form>
  </div>

</template>

<script>
import { ref , onMounted } from "vue";
import { useRoute } from "vue-router";


export default {
    name: 'GameupdateView',
    components: {
        //PaginatedBookings
    },
    setup() {
        const inventory = ref({});
        const route = useRoute();

        // const save = async function () {
        //     var response = await fetch("/api/inventoryDB", {
        //         method: "post",
        //         headers: {
        //             // 'Content-Type': 'application/x-www-form-urlencoded',
        //             'Content-Type': 'application/json'
        //         },

        //         // body: new URLSearchParams(new FormData(event.target))
        //         body: JSON.stringify(inventory.value)
        //     });

        //     console.log(response)


        // }

        // const updateBooking = async function () {

        //     await fetch("/api/inventoryDB/" + route.params.id, {
        //         method: "post",
        //         headers: {
        //             // 'Content-Type': 'application/x-www-form-urlencoded',
        //             'Content-Type': 'application/json'
        //         },

        //         // body: new URLSearchParams(new FormData(event.target))
        //         body: JSON.stringify(inventory.value)
        //     });
        onMounted(async () => {

            var response = await fetch("/api/inventoryDB/" + route.params.id);

            if (response.ok) {
                inventory.value = await response.json();
            } else {
                alert(response.statusText);
            }
        })

        const save = async function () {
            var response = await fetch("/api/inventoryDB" + this.id, {
                method: "post",
                headers: {
                    // 'Content-Type': 'application/x-www-form-urlencoded',
                    'Content-Type': 'application/json'
                },

                // body: new URLSearchParams(new FormData(event.target))
                body: JSON.stringify(inventory.value)
            });
            alert("update successfully.")
            console.log(response)


        }





        return {
        inventory,save
    }


},



}
</script>