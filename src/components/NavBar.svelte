<script lang="ts">

import {page} from "$app/stores";

</script>



<nav class="navbar navbar-expand-lg navbar-dark bg-dark">
    <div class="container-fluid">
      <a  class="navbar-brand" href="/">Galeria SK</a>
      <button class="navbar-toggler" type="button" data-bs-toggle="collapse" data-bs-target="#navbarNav" aria-controls="navbarNav" aria-expanded="false" aria-label="Toggle navigation">
        <span class="navbar-toggler-icon"></span>
      </button>
      <div class="collapse navbar-collapse" id="navbarNav">
        <ul class="navbar-nav">
          <li class="nav-item">
            <a 
                class:active = {$page.url.pathname == "/"}
                class="nav-link" 
                aria-current="page" 
                href="/">Home</a>
          </li>
          <li class="nav-item">
            <a 
                class:active = {$page.url.pathname == "/search"}
                class="nav-link" 
                href="/search">Search</a>
          </li>
        </ul>
      </div>
    </div>
  </nav>