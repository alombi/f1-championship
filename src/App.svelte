<script>
	import Header from './components/Header.svelte';
	import Home from './components/Home.svelte';
	import Footer from './components/Footer.svelte';

	//Declaring data
   let chart = [];
   let round;
	let promise;
   // Getting data
   async function getData(){
      //F1
      var request = await fetch('http://ergast.com/api/f1/current/driverStandings.json')
      var response = await request.json()
      chart = response.MRData.StandingsTable.StandingsLists[0].DriverStandings
      round = response.MRData.StandingsTable.StandingsLists[0].round
      return chart   
   }
   // Calling function
   promise = getData()
	
</script>

<main>
	<Header round={round} />
	{#await promise}
		<span></span>
	{:then chart}
		<Home chart={chart} />
		<Footer />
	{/await}
</main>