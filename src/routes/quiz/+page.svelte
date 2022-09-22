
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>
<script>
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
    ]

    function onFormSubmit() {
        question = question.map((q) => {
            if (q.answer === q.correct) {
                q.correct = q.answer
            }
            return q
        })
    }


</script>


<div>
    <form>
        <input type="text" bind:value="{question[0].label}">
        <br/>
        <input type="text" bind:value="{question[0].options[0].label}">
        <br/>
        <input type="text" bind:value="{question[0].options[1].label}">
        <br/>
        <input type="text" bind:value="{question[0].options[2].label}">
        <br/>
        <input type="text" bind:value="{question[0].options[3].label}">
        <br/>
        <input type="text" bind:value="{question[0].answer}">
        <br/>
        <input type="text" bind:value="{question[0].explain}">
        <br/>
        <button type="submit" on:click="{onFormSubmit}">Submit</button>
    </form>

    <p>{question[0].label}</p>
    <p>{question[0].options[0].label}</p>
    <p>{question[0].options[1].label}</p>
    <p>{question[0].options[2].label}</p>
    <p>{question[0].options[3].label}</p>
    <p>{question[0].answer}</p>
    <p>{question[0].explain}</p>

</div>



