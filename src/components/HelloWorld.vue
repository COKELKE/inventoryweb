<template>
  <br />
  <div class="container">

    <div class="row">
      <div class="card float-start" style="width: 35rem">
        <br />
        <br />
        <div class="container-fluid">
          <h1 class="text-start">Inventory system</h1>

          <p class="text-start">
            This is a modified jumbotron that occupies the entire horizontal space
            of its parent.
          </p>
          
        </div>
      </div>
      
      <div class="rounded float-end" style="width: 35rem">
        <apexchart width="350" type="donut" :options="options" :series="books"></apexchart>
      </div>
    </div>
    <br>
    <div class="container text-center">
      <div class="row">
        <div class="card" style="width: 18rem">
          <a href="/Books">
            <img src="https://www.readtosucceed.org/wp-content/uploads/2019/02/book-stack.png"
              class="card-img-top" /></a>
          <div class="card-body">
            <p class="card-text">
              Books
            </p>
          </div>
        </div>
        <div class="card" style="width: 18rem">
          <a href="/Games">
            <img
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQ4C-4Vq-5COoSseVCetKM7ZmfPEx3gPkoDMA&usqp=CAU"
              class="card-img-top, img-fluid" /></a>
          <div class="card-body">
            <p class="card-text">
              Games
            </p>
          </div>
        </div>
        <div class="card" style="width: 18rem">
          <a href="/Gifts">
            <img
              src="https://media.istockphoto.com/photos/gift-box-with-silver-ribbon-bow-picture-id489385290?k=20&m=489385290&s=612x612&w=0&h=xaMRA4003ZzPGXVEBTp55N9r2vZhv92ZhTezCv_j8mI="
              class="card-img-top, img-fluid" /></a>
          <div class="card-body">
            <p class="card-text">
              Gifts
            </p>
          </div>
        </div>
        <div class="card" style="width: 18rem">
          <a href="/Material">
            <img
              src="https://encrypted-tbn0.gstatic.com/images?q=tbn:ANd9GcQIsb79NoyUDNypsdZi82gzsPBYEF7MZxjNoA&usqp=CAU"
              class="card-img-top, img-fluid" /></a>
          <div class="card-body">
            <p class="card-text">
              Materials
            </p>
          </div>
        </div>
      </div>
    </div>


  </div>

</template>



<script>
// @ is an alias to /src
import { ref } from "vue";

export default {
  name: 'HelloWorldView',
  setup() {
    const options = ref({});
    const series = ref([44, 55, 41, 17, 15]);
    

    onMounted(async () => {

      //var response = await fetch("/api/bookings/aggregate/groupby");

      let token = localStorage.getItem("user");

      var response = await fetch("/api/bookings/aggregate/groupby", {
        headers: {
          "x-access-token": token
        }
      });

      if (response.ok) {
        var heroes = await response.json();

        series.value = heroes.map(a => a.count);
        options.value = { labels: heroes.map(a => a._id) };
      }
    });
    return {
      options, series,
    }
  }
}
</script>

