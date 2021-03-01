<script>
	import { onMount } from 'svelte';
	// the source data, gets set externally
	export let event = [];
	
	// activities represents the sorted list of event activities
	// "$:" means that this is a variable that gets updated when its dependency (in this case, 'event') changes
	$: activities = event.activities ? event.activities.sort((a, b) => {
		let startA = dayjs(a.start);
		let startB = dayjs(b.start);
		if (startA.isBefore(startB)) {
			return -1;
		}
		else {
			return 1;
		}
	}) : [];

	onMount(() => {
		console.log("Component onmount");
	});
	

</script>

<svelte:options tag="event-schedule" immutable={true} />

<h1>{event.name} schedule</h1>
<ul>
	{#each activities as activity}
	<li><span>{dayjs(activity.start).format('ddd H:mm')}</span> <span>{activity.name}</span></li>
	{/each}
</ul>


<style>
li {
	display: flex;
	width: 25rem;
	justify-content: space-between;
}
li > :last-child {
	width: 15rem;
}
ul > :nth-child(odd) {
	background-color: lightblue;
}
</style>