<script>
import _ from 'lodash'
import dayjs from 'dayjs'
import Select from 'svelte-select'
import { afterUpdate } from 'svelte'

import Remain from './Remain.svelte'

const currentYear = dayjs().year()
const years = [...Array(5).keys()].map(i => i + (currentYear + 1))

let selectedYear = currentYear + 1
const handleSelected = (selected) => {
  selectedYear = selected.detail.value
}
</script>

<style>
  .outer {
    height: 100vh;
    width: 100%;
    display: flex;
    flex: 1;
    flex-direction: column;
    justify-content: center;
    align-items: center;
  }
  .container {
    padding-bottom: 24%;
  }
  .select-box {
    width: 320px;
  }
  .remain {
    margin-top: 16px;
  }
  h1 {
    font-size: 1.2em;
    margin-bottom: 16px;
  }
  p {
    margin-bottom: 8px;
  }
</style>

<div class="outer">
  <div class="container">
    <h1>Display remain seconds to selected year.</h1>

    <p>Select year:</p>
    <div class="select-box">
      <!-- bind で selectedYear にバインドしても
        Remainが再レンダリングされないのでハンドラをかます -->
      <Select
        items={years}
        placeholder={currentYear + 1}
        on:select={handleSelected}
      />
    </div>

    <div class="remain">
      <Remain {selectedYear}></Remain>
    </div>
  </div>
</div>
