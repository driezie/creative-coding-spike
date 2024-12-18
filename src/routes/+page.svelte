<script>
  import Schedule from "../lib/molecule/schedule.svelte";
  import WeekSelectie from "../lib/molecule/WeekSelectie.svelte";

  export let data;
</script>

<main>
  <Schedule {data} />
</main>
