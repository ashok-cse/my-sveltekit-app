
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>
<script>


    let question = [
        {
          value: "",
            options: [
                 {
                    value: "",
                 },
                 {
                    value: "",
                 },
                 {
                    value: "",
                 },
                 {
                    value: "",
                 }
                ],
            answer: "",
            correct: "",
            explain: "",
        },
    ];



    let demoquestion = [
        {
          value: "What is the capital of India?",
            options: [
                 {
                    value: "Delhi",
                 },
                 {
                    value: "Mumbai",
                 },
                 {
                    value: "Kolkata",
                 },
                 {
                    value: "Chennai",
                 }
                ],
            answer: "Delhi",
            correct: "Delhi",
            explain: "Delhi is the capital of India",
        },
    ];
   
    let newquestion = [...question];

    function addQuestion() {
       demoquestion = [...demoquestion, {...newquestion}];
         newquestion = question
    }

</script>


<div>
    <form on:submit={addQuestion}>
        <input type="text" bind:value="{question[0].value}">
        <br/>
        <input type="text" bind:value="{question[0].options[0].value}">
        <br/>
        <input type="text" bind:value="{question[0].options[1].value}">
        <br/>
        <input type="text" bind:value="{question[0].options[2].value}">
        <br/>
        <input type="text" bind:value="{question[0].options[3].value}">
        <br/>
        <input type="text" bind:value="{question[0].answer}">
        <br/>
        <input type="text" bind:value="{question[0].correct}">
        <br/>
        <input type="text" bind:value="{question[0].explain}">
        <br/>
        <button type="submit">Submit</button>
    </form>

    <table>
        <tr>
            <th>Question</th>
            <th>Option 1</th>
            <th>Option 2</th>
            <th>Option 3</th>
            <th>Option 4</th>
            <th>Answer</th>
            <th>Explanation</th>
        </tr>
        {#each demoquestion as q}
        <tr>
            <td>{q.value}</td>
            <td>{q.options[0].value}</td>
            <td>{q.options[1].value}</td>
            <td>{q.options[2].value}</td>
            <td>{q.options[3].value}</td>
            <td>{q.answer}</td>
            <td>{q.explain}</td>
        </tr>
        {/each}
    </table>
</div>



