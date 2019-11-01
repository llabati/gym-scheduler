<script>
import { onMount } from 'svelte'
import TrainingDayDetails from './TrainingDayDetails.svelte'
import TrainingWeekSummary from './TrainingWeekSummary.svelte'
const nbOfDays = [
    { id: 1, text: 'One day', value: [ 1 ] },
    { id: 2, text: 'Two days', value: [ 1, 2 ] },
    { id: 3, text: 'Three days', value: [ 1, 2, 3 ] },
    { id: 4, text: 'Four days', value: [ 1, 2, 3, 4 ] },
    { id: 5, text: 'Five days', value: [ 1, 2, 3, 4, 5 ] },
    { id: 6, text: 'Six days', value: [ 1, 2, 3, 4, 5, 6 ] },
    { id: 7, text: 'Seven days', value: [ 1, 2, 3, 4, 5, 6, 7 ] }
]
let daysPerWeek

let summary = []
let isSummaryReady = false

function handleNewExercise(event){
    summary = [ ...summary, event.detail ]
    isSummaryReady = false
    //localStorage.setItem('summary', summary)
}

function generateSummary(){
    isSummaryReady = true
}
onMount(() => {
    if (localStorage.summary) {
        console.log('STORAGE', localStorage.summary)
        //summary = localStorage.getItem('summary')
    } 
})
</script>

<style>
.all-days {
    border: solid 2px purple;
    border-radius: 5px;
    margin: 5px;
    padding: 5px;
}
.day-details {
    background-color: rgba(0, 200, 80, .5);
    border-radius: 5px;
    margin: 5px;
    padding: 5px;
}
</style>

<div>
    <form>
        <select bind:value={ daysPerWeek }>
            { #each nbOfDays as day (day.id) }
                <option value={ day }> { day.text } per week </option>
            { /each}
        </select>
    </form>
</div>

{ #if daysPerWeek }
<div class="all-days">
    { #each daysPerWeek.value as dayNumber, index }
        <div class="day-details">
            <TrainingDayDetails title={ `day ${ ++index }` } on:add-exercise={ handleNewExercise }></TrainingDayDetails>
        </div>
    { /each }
</div>
    { #if isSummaryReady }
        <TrainingWeekSummary summary={ summary } days={ daysPerWeek.value.length }></TrainingWeekSummary>
    { /if }
        <button on:click={ generateSummary }>See summary</button>
{ /if }


