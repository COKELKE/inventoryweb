<template>
  <br>
  <nav class="navbar  bg-light container rounded-4">
    <div class="container-fluid">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="/">Home</a></li>
        <li class="breadcrumb-item active" aria-current="page"><a href="/Gifts">Gifts</a></li>
        <li class="breadcrumb-item active" aria-current="page">Gift Detail</li>
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
        <input type="text" class="form-control" id="inputEmail4" name="gifttitle" v-model="inventory.gifttitle">
      </div>
      <div class="col-md-6">
        <label for="inputPassword4" class="form-label">Category</label>
        <select id="inputState"  name="" class="form-select">
          <option selected>Open this select menu...</option>
          <option>man</option>
        </select>
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Image</label>
        <input type="text" class="form-control" id="inputCity" name="giftimage" v-model="inventory.giftimage">
      </div>
      <div class="col-md-3">
        <label for="inputCity" class="form-label">Amount</label>
        <input type="text" class="form-control" id="inputCity" name="giftamount" v-model="inventory.giftamount">
      </div>
      <div class="col-md-3">
        <label for="inputCity" class="form-label">Unit Price(HKD)</label>
        <input type="text" class="form-control" id="inputCity" name="giftprice" v-model="inventory.giftprice">
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Donated by</label>
        <input type="text" class="form-control" id="inputCity" name="giftdonate" v-model="inventory.giftdonate">
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Location</label>
        <input type="text" class="form-control" id="inputCity" name="giftlocation" v-model="inventory.giftlocation">
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Description</label>
        <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" name="giftdescription" v-model="inventory.giftdescription"></textarea>
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Address</label>
        <textarea class="form-control" id="exampleFormControlTextarea1" rows="3" name="giftaddress" v-model="inventory.giftadress"></textarea>
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
    name: 'GiftupdateView',
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