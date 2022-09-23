
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>
<script>
	let num = 0;
	let totalAttendees = [];
	let defaultAttendee = {
		question : "",
        options1 : "",
        options2 : "",
        options3 : "",
        options4 : "",
        answer : "",
        explanation : "",
	};
    
	function addPerson(attendee) {
		totalAttendees = [...totalAttendees, attendee];
	}
	
	$: attendees = Array(num).fill(defaultAttendee).map((v, i) => ({...v, id: i}));
</script>

<input bind:value={num} type="number"/>

{#each attendees as attendee, i}
<div>
	<input type="text" bind:value={attendee.question} class="bg-transparent" />
    <input type="text" bind:value={attendee.options1} class="bg-transparent" />
    <input type="text" bind:value={attendee.options2} class="bg-transparent" />
    <input type="text" bind:value={attendee.options3} class="bg-transparent" />
    <input type="text" bind:value={attendee.options4} class="bg-transparent" />
    <input type="text" bind:value={attendee.answer} class="bg-transparent" />
    <input type="text" bind:value={attendee.explanation} class="bg-transparent" />
	<button type="button" on:click={() => addPerson(attendee)}>add</button>

</div>
{/each}


<table>
    <thead>
        <tr>
            <th>Question</th>
            <th>Option1</th>
            <th>Option2</th>
            <th>Option3</th>
            <th>Option4</th>
            <th>Answer</th>
            <th>Explanation</th>
        </tr>
    </thead>
    <tbody>
        {#each totalAttendees as attendee}
        <tr>
            <td>{attendee.question}</td>
            <td>{attendee.options1}</td>
            <td>{attendee.options2}</td>
            <td>{attendee.options3}</td>
            <td>{attendee.options4}</td>
            <td>{attendee.answer}</td>
            <td>{attendee.explanation}</td>
        </tr>
        {/each}
    </tbody>
</table>