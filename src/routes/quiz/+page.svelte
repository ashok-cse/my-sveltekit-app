
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>
<script>
	let num = 0;
	let totalAttendees = [];
	let defaultAttendee = {
		id: 1,
		question: '',
		answer: '',
        explaination: '',
        options : ''
	};
	function addPerson(attendee) {
		totalAttendees = [...totalAttendees, attendee];
	}
	function removePerson(id) {
        totalAttendees = totalAttendees.filter((attendee) => attendee.id !== id);
    }


</script>



<div>
	<input type="text" bind:value={attendee.question} class="bg-transparent" placeholder="first" />
    <input type="text" bind:value={attendee.answer} class="bg-transparent" placeholder="last" />
    <input type="text" bind:value={attendee.explaination} class="bg-transparent" placeholder="last" />
    <input type="text" bind:value={attendee.options} class="bg-transparent" placeholder="last" />
    <button type="button" on:click={() => addPerson(attendee)}>add</button>
</div>


<div style="display: flex;">
	<table>
        <thead>
            <tr>
                <th>First</th>
                <th>Age</th>
            </tr>
        </thead>
        <tbody>
            {#each totalAttendees as attend}
            <tr>
                <td>{attend.first}</td>
                <td>{attend.age}</td>
            </tr>
            {/each}
    </table>
</div>