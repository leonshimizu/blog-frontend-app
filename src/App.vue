<template>
  <div id="app">
    <nav class="navbar navbar-expand-lg navbar-dark bg-dark">
  <div class="container-fluid">
    <a class="navbar-brand" href="/posts">Stassie's Blog</a>
    <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNavDropdown" aria-controls="navbarNavDropdown" aria-expanded="false" aria-label="Toggle navigation">
      <span class="navbar-toggler-icon"></span>
    </button>
    <div class="collapse navbar-collapse" id="navbarNavDropdown">
      <ul class="navbar-nav">
        <li class="nav-item">
          <a class="nav-link active" aria-current="page" href="posts/new">Create Post</a>
        </li>
        <li class="nav-item dropdown">
          <a class="nav-link dropdown-toggle" href="#" id="navbarDropdownMenuLink" role="button" data-bs-toggle="dropdown" aria-expanded="false">
            Authorization
          </a>
          <ul class="dropdown-menu" aria-labelledby="navbarDropdownMenuLink">
            <li><a class="dropdown-item" href="/login">Sign In</a></li>
            <li><a class="dropdown-item" href="/logout">Sign Out</a></li>
            <li><a class="dropdown-item" href="signup">Sign Up</a></li>
          </ul>
        </li>
      </ul>
    </div>
  </div>
    </nav>
    <div class="container">
      <router-view/>
    </div>
  </div>
</template>

<style>
body {
  font-family: 'Times New Roman', Times, serif;
  color: aliceblue;
  /* background-image: url('./assets/darkness.png'); */
}
</style>
