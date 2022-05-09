<script lang="ts">

export let url:string;
export let title: string;
export let download: string;
</script>


<div class="card" style="width: 18rem;">
    <img src={url} class="card-img-top" alt={title}>
    <div class="card-body">
      <a href={download} target="_blank " class="btn btn-success">Visualizar Imagen</a>
    </div>
  </div>

  <style>
      .card{
          height:400px;
          margin: 20px 0;
      }
      img{
          height: 80%;
      }
  </style>