<template>
  <br>
  <nav class="navbar  bg-light">
    <div class="container-fluid">
      <ol class="breadcrumb">
        <li class="breadcrumb-item"><a href="/">Home</a></li>
        <li class="breadcrumb-item active" aria-current="page">Games</li>
      </ol>
      <div class="d-flex">
        <router-link :to="`/game/detail/`"><button class="btn btn-primary " type="submit">Add</button></router-link>
      </div>
    </div>

  </nav>

<br>



<div class="container text-center">
    <div class="container row-cols-3" style="width: 56rem" v-for="booking in bookings" :key="booking._id">
      <div class="col" style="float: left">
        <div class="row"></div>
        <div class="card" >
        <router-link :to="`/game/detail/${booking._id}`">
        <img src="../assets/image.webp" class="card-img-top"
          alt="Hollywood Sign on The Hill"></router-link>
        <div class="card-body">
          <h5 class="card-title">{{ booking.gametitle }}</h5>
          <li class="list-group-item">{{ booking.gamedescription }}</li>
          <button class="btn btn-primary " style="float: right" type="submit">Borrow</button>
        </div>
      </div>
    </div>
  </div>
</div>
<br>
<div > 
  <nav aria-label="Page navigation example">
  <ul class="pagination">
    <li class="page-item"><a class="page-link" href="#">Previous</a></li>
    <li class="page-item"><a class="page-link" v-for="i in pages" :key="i" @click="fetchPage(i)">{{ i }}</a></li>
    <li class="page-item "><a class="page-link" href="#">Next</a></li>
  </ul>
</nav></div>



  <br>
</template>

<script>
import { ref, onMounted, computed } from "vue";

export default {
  //name: 'HelloWorld',
  name: 'GamesView',

  setup() {
    const bookings = ref([]);
    const lastPage = ref(0);
    const perPage = ref(2);

    const pages = computed(() => {
      var pages = [];

      for (var i = 1; i <= lastPage.value; i++) {
        pages.push(i)
      }

      return pages;
    });
    const fetchPage = async function (page) {

      var response = await fetch("/api/bookings?perPage=" + perPage.value + "&page=" + page);

      if (response.ok) {
        var data = await response.json();

        bookings.value = data.bookings;
        lastPage.value = data.pages

      } else {
        //alert(response.statusText);
      }
    };

    // onMounted(() => { fetchPage(1) });
    onMounted(function () {
      fetchPage(1);

    });

    return {
      bookings,
      pages,
      fetchPage
    };
  },
}
</script>

<style>

.pagination a{
  /* color: rgb(24, 154, 241); */
  float: left;
  padding: 8px 16px;
  text-decoration: none;
}
</style>

