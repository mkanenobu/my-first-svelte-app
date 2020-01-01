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
  h1 { margin-bottom: 16px; }
  p { margin-bottom: 8px; }
  .container {
    margin: 16px;
  }
</style>

<div class="container">
  <h1>Display remain seconds to selected year.</h1>

  <p>Select year:</p>
  <!-- bind で selectedYear にバインドしても，
    Remainが再レンダリングされないのでハンドラをかます -->
  <Select
    items={years}
    placeholder={currentYear + 1}
    on:select={handleSelected}
  />

  <!--  not response reactive when props changed  -->
  <Remain {selectedYear}></Remain>
</div>
