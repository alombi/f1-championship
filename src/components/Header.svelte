<script>
   export let round = 'Loading...';
   const months = ['January', 'February', 'March', 'April', 'May', 'June', 'July', 'August', 'September', 'October', 'November', 'December']
   let day, month, year;
   let now = new Date()
   day = now.getDate()
   month = months[now.getMonth()]
   year = now.getFullYear()
</script>

<div class="fake"></div>
<header>
   <div class="logo">
      <i class="fas fa-flag-checkered"></i> F1 Championship
   </div>
   <div class="options">
      <p>Races done: {round}</p>
      <p class="no_mobile" id="date">{day} {month} {year}</p>
   </div>
</header>