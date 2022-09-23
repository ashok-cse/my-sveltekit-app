<svelte:head>
    <title>Panel</title>
    <meta name="description" content="Quiz">
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
    

<div>
    <input type="text" bind:value={question.label} class="bg-transparent" placeholder="Enter Your Question" />
    <input type="text" bind:value={option.value} class="bg-transparent" placeholder="Option" />
    <input type="checkbox" bind:checked={option.isCorrect} />
    <button type="button" on:click={addNewOption}>Add Option</button>
    <button type="button" on:click={addNewQuestion}>Add Question</button>
</div>

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
        {#each questions as question, i}
        <tr>
            <td>{question.label}</td>
            {#each question.options as option, i}
            <td>{option.value}</td>
            {/each}
        </tr>
        {/each}
    </tbody>