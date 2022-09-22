
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>
<script>
  import Counter from "../../lib/Counter.svelte";


    let question = [
        {
          label: "",
            options: [
                 {
                    label: "",
                    value: "",
                 },
                 {
                    label: "",
                    value: "",
                 },
                 {
                    label: "",
                    value: "",
                    correct: false
                 },
                 {
                    label: "",
                    value: "",
                 }
                ],
            answer: "",
            correct: "",
            explain: "",
        },
    ];

    let newquestion = [...question];

    let demoquestion = [
        {
          label: "What is the capital of India?",
          value: "What is the capital of India?",
            options: [
                 {
                    label: "Delhi",
                    value: "Delhi",
                 },
                 {
                    label: "Mumbai",
                    value: "Mumbai",
                 },
                 {
                    label: "Kolkata",
                    value: "Kolkata",
                    correct: false
                 },
                 {
                    label: "Chennai",
                    value: "Chennai",
                 }
                ],
            answer: "Delhi",
            correct: "Delhi",
            explain: "Delhi is the capital of India",
        },
    ];
   
   
    
    function onFormSubmit() {
         demoquestion = [...demoquestion, [...newquestion]]
            
             newquestion = question
    }



</script>


<div>
    <form>
        <input type="text" bind:value="{question[0].value}" bind:label="{question[0].label}">
        <br/>
        <input type="text" bind:value="{question[0].options[0].value}" bind:label="{question[0].options[0].label}">
        <br/>
        <input type="text" bind:label="{question[0].options[1].label}" bind:value="{question[0].options[1].value}" >
        <br/>
        <input type="text" bind:label="{question[0].options[2].label}" bind:value="{question[0].options[2].value}" >
        <br/>
        <input type="text" bind:label="{question[0].options[3].label}" bind:value="{question[0].options[3].value}" >
        <br/>
        <input type="text" bind:value="{question[0].answer}" >
        <br/>
        <input type="text" bind:value="{question[0].correct}" >
        <br/>
        <input type="text" bind:value="{question[0].explain}" >
        <br/>
        <button type="submit" on:click="{onFormSubmit}">Submit</button>
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
            <td>{q.label}</td>
            <td>{q.options[0].label}</td>
            <td>{q.options[1].label}</td>
            <td>{q.options[2].label}</td>
            <td>{q.options[3].label}</td>
            <td>{q.answer}</td>
            <td>{q.explain}</td>
        </tr>
        {/each}
    </table>

</div>



