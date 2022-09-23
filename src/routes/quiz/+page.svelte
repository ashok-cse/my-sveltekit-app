
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>

<style>
    .quiz-form {
    border-style: solid;
    /* margin-bottom: 10px; */
    /* margin-left: 10px; */
    padding: 10px;
    /* width: 50%; */
    margin: auto;
    width: 50%;
    /* border: 3px solid green; */
    /* padding: 10px; */
}

.quiz-table {
    border-style: solid;
    /* margin-bottom: 10px; */
    /* margin-left: 10px; */
    padding: 20px;
    /* width: 50%; */
    margin: auto;
    width: 70%;
    /* border: 3px solid green; */
    /* padding: 10px; */
}

body > table{
    width: 80%;
}

table{
    border-collapse: collapse;
}
table.list{
    width:100%;
}

td, th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
}
tr:nth-child(even),table.list thead>tr {
    background-color: #dddddd;
}

input[type=text], input[type=number] {
    width: 100%;
    padding: 8px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
}

input[type=submit] {
    width: 30%;
    background-color: black;
    color: white;
    padding: 10px 18px;
    /* margin: 0px 0; */
    border: none;
    border-radius: 5px;
    cursor: pointer;
}

form div.form-action-buttons{
    text-align: right;
}

a{
    cursor: pointer;
    text-decoration: underline;
    color: #0000ee;
    margin-right: 4px;
}

label.validation-error{
    color:   red;
    margin-left: 5px;
}

.hide{
    display:none;
}
</style>


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

    function deleteQuestion (index) {
        questions = questions.filter((q, i) => i !== index)
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
     <table class="quiz-table">
        <thead>
            <tr>
                <th>Question</th>
                <th>Options</th>
                <th>Actions</th>
            </tr>
        </thead>
        <tbody>
            {#each questions as question}
                <tr>
                    <td>{question.label}</td>
                    <td>
                        {#each question.options as option}
                            <div>
                                <span>{option.value}</span>
                                <span>{option.isCorrect}</span>
                            </div>
                        {/each}
                    </td>
                    <td>
                        <a>Edit</a>
                        <a on:click="{deleteQuestion}">Delete</a>
                    </td>
                </tr>
            {/each}
        </tbody>
     </table>
    </div>
