<script>
import TrainingDays from './components/TrainingDays.svelte'
export let title;
</script>

<style>
.container {
	width: 66%;
	margin: 10px auto;
}
	h1 {
		color: purple;
		text-align: center;
	}
</style>
<div class="container">
	<h1>{ title }</h1>
	<TrainingDays></TrainingDays>
</div>
