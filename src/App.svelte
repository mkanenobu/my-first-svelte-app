<script>
import dayjs from 'dayjs'
import { onMount } from 'svelte'

let time = dayjs()
$: nextYear = time.add(1, 'years').format('YYYY')
$: nextYearStart = dayjs(`${nextYear}-01-01 00:00`).unix()
$: current = time.unix()

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
  .inner {
    text-align: center;
    width: 180px;
    border: 1px solid;
    border-radius: 16px;
  }
  p { font-size: 24px; }
</style>

<div class="container">
  <span class="inner">
    <p>{nextYear}年まで</p>
    <p>あと{nextYearStart - current}秒</p>
  </span>
</div>
