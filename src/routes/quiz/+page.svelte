
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
            explain: "",
        },
    ]

    function onFormSubmit() {
        console.log(question)
    }

    function onFormReset() {
        console.log("reset")
    }

    function onFormChange() {
        console.log("change")
    }

    function onFormInput() {
        console.log("input")
    }

    function onFormInvalid() {
        console.log("invalid")
    }

    function onFormValid() {
        console.log("valid")
    }


</script>


<div>
    <form>
        <input type="text" bind:value="{question[0].label}">
        <input type="text" bind:value="{question[0].options[0].label}">
        <input type="text" bind:value="{question[0].options[1].label}">
        <input type="text" bind:value="{question[0].options[2].label}">
        <input type="text" bind:value="{question[0].options[3].label}">
        <input type="text" bind:value="{question[0].answer}">
        <input type="text" bind:value="{question[0].explain}">
        <button type="submit" on:click="{onFormSubmit}">Submit</button>
    </form>
</div>



