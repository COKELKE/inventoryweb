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
        <input type="text" class="form-control" id="giftimage" name="giftimage" v-model="inventory.giftimage">
      </div>
      <div class="col-md-3">
        <label for="inputCity" class="form-label">Amount</label>
        <input type="text" class="form-control" id="giftamount" name="giftamount" v-model="inventory.giftamount">
      </div>
      <div class="col-md-3">
        <label for="inputCity" class="form-label">Unit Price(HKD)</label>
        <input type="text" class="form-control" id="giftprice" name="giftprice" v-model="inventory.giftprice">
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Donated by</label>
        <input type="text" class="form-control" id="giftdonate" name="giftdonate" v-model="inventory.giftdonate">
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Location</label>
        <input type="text" class="form-control" id="giftlocation" name="giftlocation" v-model="inventory.giftlocation">
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Description</label>
        <textarea class="form-control" id="giftdescription" rows="3" name="giftdescription" v-model="inventory.giftdescription"></textarea>
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Address</label>
        <textarea class="form-control" id="giftaddress" rows="3" name="giftaddress" v-model="inventory.giftadress"></textarea>
      </div>
      <div class="col-12">
        <button type="submit" class="btn btn-primary">Save</button>
      </div>
    </form>
  </div>
</template>

<script>
import { ref } from 'vue'

export default {
    name: 'BookdetailsView',
    components: {
        //PaginatedBookings
    },
    setup() {
        const inventory = ref({});

        const save = async function () {
            var response = await fetch("/api/inventoryDB", {
                method: "post",
                headers: {
                    // 'Content-Type': 'application/x-www-form-urlencoded',
                    'Content-Type': 'application/json'
                },

                // body: new URLSearchParams(new FormData(event.target))
                body: JSON.stringify(inventory.value)
            });

            console.log(response)


        }

        return {
            inventory, save
        }

    }
}
</script>