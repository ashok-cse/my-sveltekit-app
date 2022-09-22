<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>

<script>
	let quiz = [
		{ question: '', options1: '', options2: '', options3: '', options4: '', correct: '',  },
	];

    let prefix = '';
	let question = '';
	let options1 = '';
	let options2 = '';
	let options3 = '';
	let options4 = '';
	let correct = '';
	let i = 0;

	$: filteredQues = prefix
		? quiz.filter(ops => {
			const name = `${ops.options1}, ${ops.options2}, ${ops.options3}, ${ops.options4}`;
			return name.toLowerCase().startsWith(prefix.toLowerCase());
		})
		: quiz;

	$: selected = filteredQues[i];


	function create() {
		quiz = quiz.concat({ question, options1, options2, options3, options4, correct });
		i = quiz.length - 1;
		question = options1 = options2 = options3 = options4 = correct = '';
	}

	function update() {
		selected.question = question;
		selected.options1 = options1;
		selected.options2 = options2;
		selected.options3 = options3;
		selected.options4 = options4;
		selected.correct = correct;

		quiz = quiz;
	}

	function remove() {
		// Remove selected person from the source array (people), not the filtered array
		const index = quiz.indexOf(selected);
		quiz = [...quiz.slice(0, index), ...quiz.slice(index + 1)];

		question = options1 = options2 = options3 = options4 = correct = '';
		i = Math.min(i, filteredQues.length - 2);
	}
</script>

<input placeholder="filter prefix" bind:value={prefix}>

<select bind:value={i} size={5}>
	{#each filteredQues as ques, i}
		<option value={i}>{ques.question}, {ques.options1}, {ques.options2}, {ques.options3}, {ques.options4}, {ques.correct}</option>
	{/each}
</select>

<label><input bind:value={question} placeholder="question">question</label>
<label><input bind:value={options1} placeholder="options1">options1</label>
<label><input bind:value={options2} placeholder="options2">options2</label>
<label><input bind:value={options3} placeholder="options3">options3</label>
<label><input bind:value={options4} placeholder="options4">options4</label>
<label><input bind:value={correct} placeholder="correct">Correct</label>


<div class='buttons'>
	<button on:click={create} disabled="{!question || !options1 || !options2 || !options3 || !options4 || !correct}">create</button>
	<button on:click={update} disabled="{!question || !options1 || !options2 || !options3 || !options4 || !correct || !selected}">update</button>
	<button on:click={remove} disabled="{!selected}">delete</button>
</div>

<style>
	* {
		font-family: inherit;
		font-size: inherit;
	}

	input {
		display: block;
		margin: 0 0 0.5em 0;
	}

	select {
		float: left;
		margin: 0 1em 1em 0;
		width: 14em;
	}

	.buttons {
		clear: both;
	}
</style>


