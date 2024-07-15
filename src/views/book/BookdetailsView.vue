<template>
    <br>
    <nav class="navbar  bg-light container rounded-4">
        <div class="container-fluid">
            <ol class="breadcrumb">
                <li class="breadcrumb-item"><a href="/">Home</a></li>
                <li class="breadcrumb-item active" aria-current="page"><a href="/Books">Books</a></li>
                <li class="breadcrumb-item active" aria-current="page">Book Detail</li>
            </ol>
            <div class="d-flex">

            </div>
        </div>

    </nav>

    <br>

    <br>

    <div class="container">
        <form class="row g-3" action="/api/inventoryDB" method="POST" @submit.prevent="save">
            <div class="col-md-6">
                <label for="inputCity" class="form-label">Title</label>
                <input type="text" class="form-control" id="booktitle" name="booktitle" v-model="inventory.booktitle">
            </div>
            <div class="col-md-6">
                <label for="inputCity" class="form-label">Category</label>
                <select aria-label="Default select example" onchange="CategorySelected(this.value)" class="form-select"
                    id="bookcategory" name="bookcategory" v-model="inventory.bookcategory">
                    <option selected>Open this select menu...</option>
                    <option>man</option>
                    <option>woman</option>
                    <option>kids</option>
                </select>
            </div>
            <div class="col-md-6">
                <label for="inputCity" class="form-label">Author</label>
                <input type="text" class="form-control" id="author" name="author" v-model="inventory.author">
            </div>
            <div class="col-md-6">
                <label for="inputCity" class="form-label">Publisher</label>
                <input type="text" class="form-control" id="bookpublisher" name="bookpublisher"
                    v-model="inventory.bookpublisher">
            </div>
            <div class="col-md-6">
                <label for="inputCity" class="form-label">Year</label>
                <input type="text" class="form-control" id="year" name="year" v-model="inventory.year">
            </div>
            <div class="col-md-6">
                <label for="inputCity" class="form-label">Location</label>
                <input type="text" class="form-control" id="location" name="location" v-model="inventory.booklocation">
            </div>
            <div class="col-md-6">
                <label for="inputCity" class="form-label">ISBN</label>
                <input type="text" class="form-control" id="isbn" name="bookisbn" v-model="inventory.bookisbn">
            </div>
            <div class="col-md-6">
                <label for="inputCity" class="form-label">Image</label>
                <input type="text" class="form-control" id="bookimage" name="bookimage" v-model="inventory.bookimage">
            </div>
            <div class="form-group col-md-6">
                <label for="exampleFormControlTextarea1">Description</label>
                <textarea class="form-control" id="bookdescription" name="bookdescription" rows="3"
                    v-model="inventory.bookdescription"></textarea>
            </div>
            <div class="form-group col-md-6">
                <label for="exampleFormControlTextarea1">Remark</label>
                <textarea class="form-control" id="remark" name="bookremark" rows="3"
                    v-model="inventory.bookremark"></textarea>
            </div>
            <div>
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
