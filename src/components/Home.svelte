<script>
   export let chart;
</script>


<div class="home_container">
   {#each chart as driver}
      <div class="item">
         <h3><span class="positioning">{driver.points} Pts</span> {driver.Driver.givenName} {driver.Driver.familyName} - {driver.Constructors[0].name}</h3>
      </div>
   {/each}
</div>