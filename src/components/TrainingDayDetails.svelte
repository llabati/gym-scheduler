<script>
import { createEventDispatcher } from 'svelte'

const dispatch = createEventDispatcher()

export let title
let exercise = {
    activity: '',
    sets: 4,
    reps: 10
}
let exercises = []

function handleSubmit(){
    exercises = [ ...exercises, { ...exercise } ]
    dispatch('add-exercise', { ...exercise, title })

    exercise = {
    activity: '',
    sets: 4,
    reps: 10
    }
}
function stringify(object){
    return JSON.stringify(object)
}
function stringifyArray(array) {
    let res = [];
    for (let obj of array) {
      res = [ ...res, stringify(obj) ];
    }
    return res;
  }

// || 
</script>

<style>
h2 {
    color: rgb(0, 200, 80);
}
form {
    display: inline-block;
    width: 45%;
    margin: 10px 5px 10px 0px;
}
#right {
    display: inline-block;
    width: 45%;
    margin: 10px 5px 10px 5px;
}

ul {
    list-style-type: none;
}

.add-btn {
    background-color: rgb(0, 200, 80);
    color: white;
    padding: 5px;
    border-radius: 5px;
}
</style>

<div>
<h2> { title } </h2>
<form on:submit|preventDefault={handleSubmit}>
    <div>
        <label for="activity">Activity</label>
        <input type="text" id="activity" bind:value={exercise.activity}>
    </div>
    <div>
        <label for="sets">Sets</label>
        <input type="number" id="sets" bind:value={exercise.sets}>
    </div>
    <div>
        <label for="reps">Reps</label>
        <input type="number" id="reps" bind:value={exercise.reps}>
    </div>
    <div>
        <button type="submit" class="add-btn">Add exercise</button>
    </div>
</form>
</div>
<div id="right">
    <ul>
        { #each exercises as ex }
            <li><strong>{ ex.activity }: </strong>{ ex.sets } sets of { ex.reps } reps</li>
        { /each }
    </ul>
</div>