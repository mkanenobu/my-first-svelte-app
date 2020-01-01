<script>
import dayjs from 'dayjs'
import { onMount } from 'svelte'

export let selectedYear

let time = dayjs()
$: nextYearStart = dayjs(`${selectedYear}-01-01 00:00`).unix()
$: current = time.unix()
$: remainSeconds = nextYearStart - current

// set timer on mount
onMount(() => {
  const interval = setInterval(() => {
    time = dayjs()
  }, 1000)

  return () => {
    clearInterval(interval);
  }
})
</script>

<style>
  .container {
    display: flex;
    flex-direction: column;
    justify-content: center;
    align-items: center;
    width: auto;
    height: 100vh;
  }
  p { font-size: 24px; }
</style>

<div class="container">
  <p>Remain {remainSeconds} seconds to {selectedYear}</p>
</div>

