<template>
  <br>
  <nav class="navbar  bg-light container rounded-4">
    <div class="container-fluid">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="/">Home</a></li>
        <li class="breadcrumb-item active" aria-current="page"><a href="/Materials">Materials</a></li>
        <li class="breadcrumb-item active" aria-current="page">Material Detail</li>
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
        <input type="text" class="form-control" id="materialtitle" name="materialtitle" v-model="inventory.materialtitle">
      </div>
      <div class="col-md-6">
        <label for="inputPassword4" class="form-label">Category</label>
        <select id="materialcategory" class="form-select" name="materialcategory" v-model="inventory.materialcategory">
          <option selected>Open this select menu...</option>
          <option>...</option>
        </select>
      </div>
      <div class="col-md-6">
        <label for="inputCity" class="form-label">Image</label>
        <input type="text" class="form-control" id="materialimage" name="materialimage" v-model="inventory.materialimage">
      </div>
      <div class="col-md-3">
        <label for="inputCity" class="form-label">Amount</label>
        <input type="text" class="form-control" id="materialamount" name="materialamount" v-model="inventory.materialamount">
      </div>
      <div class="col-md-3">
        <label for="inputCity" class="form-label">Location</label>
        <input type="text" class="form-control" id="materiallocation" name="materiallocation" v-model="inventory.materiallocation">
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Description</label>
        <textarea class="form-control" id="materialdescription" rows="3" name="materialdescription" v-model="inventory.materialdescription"></textarea>
      </div>
      <div class="form-group col-md-6">
        <label for="exampleFormControlTextarea1">Address</label>
        <textarea class="form-control" id="materialdaddress" rows="3" name="materialdaddress" v-model="inventory.materialdaddress"></textarea>
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