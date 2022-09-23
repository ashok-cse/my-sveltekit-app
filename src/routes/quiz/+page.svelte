
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

    <div>
        <h1>Quiz Panel</h1>
        <div>
            <h2>Question</h2>
            <input type="text" bind:value={question.label} />
            <h2>Options</h2>
            <div>
                <input type="text" bind:value={option.value} />
                <input type="checkbox" bind:checked={option.isCorrect} />
                <button on:click={addNewOption}>Add Option</button>
            </div>
            <div>
                {#each question.options as option}
                    <div>
                        <span>{option.value}</span>
                        <span>{option.isCorrect}</span>
                    </div>
                {/each}
            </div>
            <button on:click={addNewQuestion}>Add Question</button>
        </div>
        <div>
            <h2>Questions</h2>
            {#each questions as question}
                <div>
                    <span>{question.label}</span>
                    <div>
                        {#each question.options as option}
                            <div>
                                <span>{option.value}</span>
                                <span>{option.isCorrect}</span>
                            </div>
                        {/each}
                    </div>
                </div>
            {/each}
        </div>
    </div>
