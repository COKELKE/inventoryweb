<template>
  <nav class="navbar navbar-expand-lg bg-light">
    <div class="container-fluid">
      <a class="navbar-brand" href="/">Inventory</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarSupportedContent"
        aria-controls="navbarSupportedContent" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarSupportedContent">
        <ul class="navbar-nav me-auto mb-2 mb-lg-0">
          <li class="nav-item">
            <a class="nav-link active" aria-current="page" href="/Books">Books</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" href="/Games">Games</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" href="/Gifts">Gifts</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" href="/Material">Materials</a>
          </li>
          <li class="nav-item">
            <a class="nav-link active" href="/User">User</a>
          </li>
        </ul>
        <form class="d-flex" role="search">
          <!-- <input
            class="form-control me-2"
            type="search"
            placeholder="Search"
            aria-label="Search"
          />
          <router-link :to="`/Search`"><button class="btn btn-outline-success" type="submit">Search</button></router-link> -->
          <router-link :to="`/Login`"><button class="btn btn-primary" type="submit">Login</button></router-link>
          <button type="button" class="btn btn-primary" @click="logout">Log Out</button>
        </form>
      </div>
    </div>
  </nav>
  <router-view />
</template>

<script>

export default {
  name: 'HelloWorldView',
  setup() {
    
    const logout = function () {
      localStorage.removeItem('user');
      location.reload()
    }


    return {
      logout
    }
  }
}
</script>

<style>
#app {
  font-family: Avenir, Helvetica, Arial, sans-serif;
  -webkit-font-smoothing: antialiased;
  -moz-osx-font-smoothing: grayscale;
  text-align: center;
  color: #2c3e50;
}

nav {
  padding: 30px;
}

nav a {
  font-weight: bold;
  color: #2c3e50;
}

nav a.router-link-exact-active {
  color: #42b983;
}
</style>
