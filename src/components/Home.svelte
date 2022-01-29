<script>
  export let chart, round;
	import { races } from '../store.js'
</script>


<div class="home_container">
	{#if $races - round != 0}
		<h1 class="no_mobile">Formula One World Championship</h1>
	{:else}
		
		<h1 class="winner"><i class="fas fa-trophy"></i><br>{chart[0].Driver.givenName} {chart[0].Driver.familyName} is the World champion!</h1>
	{/if}
	<div class="list">
		{#each chart as driver}
			<div class="item">
				<h3><span class="positioning">{driver.points} Pts</span> {driver.Driver.givenName} {driver.Driver.familyName} - {driver.Constructors[0].name}</h3>
				</div>
		{/each}
	</div>
</div>