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
        <apexchart width="350" type="donut" :options="options" :series="series"></apexchart>
      </div>
    </div>
    <br>

 
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

        return {
            options, series
        }
    }
}
</script>

