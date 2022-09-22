
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>
<script>

let questions = []
let question = {
	label: '',
	options: []
}
let option = { value: '', isCorrect: false }
function addNewOption() {
	// console.log('option', option)
	question.options = [...question.options, { ...option }]
	// console.log('question.options', question.options)
	cleaOption()
}
function addNewQuestion() {
	console.log('question', question)
	questions = [...questions, { ...question }]
	console.log('questions', questions)
	cleaQuestion()
}
function cleaOption() {
	option.value = ''
	option.isCorrect = false
}
function cleaQuestion() {
	question.label = ''
	question.options = []
}
</script>
<div class="container mx-auto min-h-screen max-w-xl p-3 text-black sm:p-10">
	<h1 class="mb-4 text-lg font-bold">Add Questions</h1>
	<div class="flex flex-col gap-2 rounded-3xl bg-black p-6 shadow-lg">
		<label>
			<h2 class="mb-2 font-semibold text-white">Question</h2>
			<input type="text" bind:value="{question.label}" class="w-full" />
		</label>
		{#if question.options?.length > 0}
			<ul class="text-white">
				{#each question.options as o}
					<li>{o.value}:{o.isCorrect}</li>
				{/each}
			</ul>
		{/if}
		<label for="option">
			<h2 class="mb-2 font-semibold text-white">Option</h2>
			<div class="flex items-center gap-2">
				<input id="option" type="text" bind:value="{option.value}" class=" w-full" />
				<input type="checkbox" bind:checked="{option.isCorrect}" class="h-6 w-6" />
			</div>
		</label>
		<button
			type="submit"
			class="max-w-max bg-white px-2 py-1 focus:outline-none"
			on:click="{addNewOption}">
			Add New Option
		</button>
		<button
			type="button"
			class="max-w-max bg-white px-2 py-1 focus:outline-none"
			on:click="{addNewQuestion}">
			Add New Question
		</button>
	</div>
	<br />
	<br />
	<br />
	<table>
		<thead>
			<tr class="divide-x">
				<th class="p-3">#</th><th class="p-3">questions</th><th class="p-3">options</th>
			</tr>
		</thead>
		<tbody>
			{#each questions as q, qx}
				<tr>
					<td class="p-3">{qx + 1}</td>
					<td class="p-3">{q.label}</td>
					<td class="p-3">
						<ul class="flex flex-col gap-1">
							{#each q.options as o}
								<li class="flex items-center gap-2">
									<span>{o.value}</span>
									:
									<span>{o.isCorrect}</span>
								</li>
							{/each}
						</ul>
					</td>
				</tr>
			{/each}
		</tbody>
	</table>
</div>


