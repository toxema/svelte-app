<script>
  export let name;
  export let data;

  import { onMount } from "svelte";
  import axios from "axios";
  let canvasElement;

  function getAllData() {
    const url = "http://rezonansmuhendislik.com/webcloud/servis.php?cmd=getAll";
    axios.get(url, {}).then(obj => {
      data = obj.data;
      console.log(data);
    });
  }

  onMount(() => {
    console.log("obj mounted");
    getAllData();
    window.setInterval(() => {
                    getAllData();
                }, 3000)
  });
</script>
<!-- ########## STYLE CONFIGRATION      ##################### -->
<style>
  tr.rows:hover {
    background-color: rgb(225, 233, 243);
  }
</style>
<!-- ########## STYLE CONFIGRATION      ##################### -->


<div id="app" class="container">
  <div class="fix-top bg-dark">
    <h1 class="text-white">Svelte</h1>
  </div>
  <table class="table">
    <thead class="thead-dark">
      <tr>
        <th scope="col">#Dev ID</th>
        <th scope="col">Name</th>
        <th scope="col">Tank 1</th>
        <th scope="col">Tank 2</th>
        <th scope="col">Firm</th>
        <th scope="col">Last Update</th>
      </tr>
    </thead>
    <tbody>
      {#each data as tank}
        <tr class="rows">
          <th scope="row">{tank.uid}</th>
          <td>{tank.name}</td>
          <td>%{tank.tank1}</td>
          <td>%{tank.tank2}</td>
          <td>{tank.firm}</td>
          <td>{tank.last_update}</td>
        </tr>
      {/each}
    </tbody>
  </table>

</div>
