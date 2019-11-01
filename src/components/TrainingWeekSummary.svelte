<script>
import { onMount } from 'svelte'

export let summary
export let days

let formattedData
let isDataFormatted = false

function prepareSummary(){
  if (summary){
    formattedData = summary.reduce((acc, cur) => {
        if (Object.keys(acc).includes(cur.title)){
            acc[cur.title] = [ ...acc[cur.title], cur ]
        } else acc[cur.title] = [ cur ]
        return acc
    }, {})
    isDataFormatted = true
  }
}

onMount(() => {
    prepareSummary()
})

</script>

<style>
h2 {
    color: purple;
}
</style>


{ #if isDataFormatted }
  <h2>Summary</h2>
  { #if summary.length }
    { #each Object.keys(formattedData) as day }
      <h2>{ day }</h2>
      { #each formattedData[day] as ex }
        <p>{ ex.activity }: { ex.sets } sets of { ex.reps } reps</p>
      { /each }
    { /each }
  { :else }
    <div>Missing data: please add exercises</div>
  { /if }
{ /if }