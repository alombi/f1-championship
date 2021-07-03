<script>
   export let chart;
</script>


<div class="home_container">
   <h1 class="no_mobile">Chart</h1>
   <div class="list">
      {#each chart as driver}
         <div class="item">
            <h3><span class="positioning">{driver.points} Pts</span> {driver.Driver.givenName} {driver.Driver.familyName} - {driver.Constructors[0].name}</h3>
         </div>
      {/each}
   </div>
</div>