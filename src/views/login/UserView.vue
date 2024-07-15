<template>
    <br>
    <nav class="navbar  bg-light">
        <div class="container-fluid">
            <ol class="breadcrumb">
                <li class="breadcrumb-item"><a href="/">Home</a></li>
                <li class="breadcrumb-item active" aria-current="page">User</li>
            </ol>
            <div class="d-flex">
                <router-link :to="`/user/details`"><button class="btn btn-primary " type="submit">Add</button>
                </router-link>
            </div>
        </div>

    </nav>

    <br>
    <div class="container">
        <div class="container text-center">
            <div class="row">

                <div class="card text-center" style="width: 20rem;" v-for="user in user" :key="user._id">
                    <div class="card-body">
                        <h5 class="card-title">{{ user.fullname }}</h5>
                        <p class="card-text">{{ user.email }}</p>
                        <router-link :to="`/user/detail/${user._id}`">
                            <a>Update</a></router-link>
                    </div>
                </div>
                <!-- <div class="card text-center" style="width: 20rem;">
                    <div class="card-body">
                        <h5 class="card-title">Full Nume</h5>
                        <p class="card-text">email address</p>
                        <a href="#">Update</a>
                    </div>
                </div>  -->


            </div>
        </div>
    </div>
</template>
  
<script>
import { ref, onMounted, computed } from "vue";

// export default {
//     name: 'UserView',
//     setup() {
//         const user = ref({});

//         onMounted(async () => {

//             var response = await fetch("/api/usershow");

//             if (response.ok) {
//                 user.value = await response.json();
//             } else {
//                 alert(response.statusText);
//             }
//         })

//         return {
//             user
//         }
//     }
// }

export default {
  //name: 'HelloWorld',
  name: 'UserView',

  setup() {
    const user = ref([]);
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

      var response = await fetch("/api/usershows?perPage=" + perPage.value + "&page=" + page);

      if (response.ok) {
        var data = await response.json();

        user.value = data.bookings;
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
      user,
      pages,
      fetchPage
    };
  },
}

</script>