<script>
  export let round = 'Loading...';
  import { races } from '../store.js';
  let lastRace, lastRaceWinner, lastRaceDate;
  let totalRaces, nextRaceLocality, nextRaceDate;
  let nextRace;
  async function getLastRace(){
    var request = await fetch('https://ergast.com/api/f1/current/last/results.json')
    var response = await request.json()
    let raceName = response.MRData.RaceTable.Races[0].raceName;
    lastRaceDate = response.MRData.RaceTable.Races[0].date;
    lastRaceWinner = response.MRData.RaceTable.Races[0].Results[0].Driver.familyName;
    return `${raceName}`
  }
  async function getNextRace(){
    var request = await fetch('https://ergast.com/api/f1/current/next.json')
    var response = await request.json()
    let raceName = response.MRData.RaceTable.Races[0].raceName;
    nextRaceLocality = `${response.MRData.RaceTable.Races[0].Circuit.Location.locality},   ${response.MRData.RaceTable.Races[0].Circuit.Location.country}`
    nextRaceDate = response.MRData.RaceTable.Races[0].date
    return raceName
  }
  async function getTotalRaces(){
    var request = await fetch('https://ergast.com/api/f1/current.json')
    var response = await request.json()
    let totalRaces = response.MRData.total
    races.set(response.MRData.total)
    return totalRaces
  }
  totalRaces = getTotalRaces()
  lastRace = getLastRace()
  nextRace = getNextRace()
</script>


<div class="sidebar">
   <div class="logo">
      <i class="fas fa-flag-checkered"></i> F1 Championship
   </div>
   <div class="info">
      <h3><i class="fas fa-info-circle icon"></i> Informations</h3>
      <hr>

      <p>
         <span class="label">Races done:</span> {round}
      </p>
      {#await totalRaces}
         <p>
            <span class="label">Races to go:</span> Loading...
         </p>
      {:then totalRaces}
         <p>
            <span class="label">Races to go:</span> {totalRaces - round}
         </p>
      {/await}
      <p>
         <span class="label">Season:</span> 2021
      </p>
   </div>

   <div class="info">
      <h3><i class="fas fa-backward icon"></i> Last race</h3>
      <hr>

      {#await lastRace}
      <p>
         <span class="label">Gran prix:</span> Loading...
      </p>
      <p>
         <span class="label">Winner:</span> Loading...
      </p>
      <p>
         <span class="label">Date:</span> Loading...
      </p>
      {:then lastRace}
         <p>
            <span class="label">Gran prix:</span> {lastRace}
         </p>
         <p>
            <span class="label">Winner:</span> {lastRaceWinner}
         </p>
         <p>
            <span class="label">Date:</span> {lastRaceDate}
         </p>
      {/await}
   </div>
   <div class="info">
      <h3><i class="fas fa-forward icon"></i> Next race</h3>
      <hr>
      {#await nextRace}
         <p>
            <span class="label">Gran prix:</span> Loading...
         </p>
         <p>
            <span class="label">Locality:</span> Loading...
         </p>
         <p>
            <span class="label">Date:</span> Loading...
         </p>
      {:then nextRace}
         <p>
            <span class="label">Gran prix:</span> {nextRace}
         </p>
         <p>
            <span class="label">Locality:</span> {nextRaceLocality}
         </p>
         <p>
            <span class="label">Date:</span> {nextRaceDate}
         </p>
      {/await}
   </div>
</div>

<style>
   .logo{
      padding-top: 20px;
   }
   .icon{
      font-size: 14px;
   }
</style>