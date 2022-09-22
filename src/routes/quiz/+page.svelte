
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>
<script>
	let num = 0;
	let totalAttendees = [];
	let defaultAttendee = {
		id: 1,
		first: '',
		age: undefined
	};
	function addPerson(attendee) {
		totalAttendees = [...totalAttendees, attendee];
	}
	
	$: attendees = Array(num).fill(defaultAttendee).map((v, i) => ({...v, id: i}));
</script>

<input bind:value={num} type="number"/>

{#each attendees as attendee, i}
<div>
	<input type="text" bind:value={attendee.first} class="bg-transparent" placeholder="first" />
	<input type="number" bind:value={attendee.age} class="bg-transparent" placeholder="age" />
	<button type="button" on:click={() => addPerson(attendee)}>add</button>
</div>
{/each}

<div style="display: flex;">
	<div style="margin-right: 20px; flex-grow: 1">
		<h1>attendees</h1>
		<pre>{JSON.stringify(attendees, null, 2)}</pre>
	</div>
	<div style="flex-grow: 1">
		<h1>totalAttendees</h1>
		<pre>{JSON.stringify(totalAttendees, null, 2)}</pre>
	</div>
</div>