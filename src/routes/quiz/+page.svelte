<script>
  let questions = [];
  let question = {
    id : 0,
    label: "",
    options: [],
    explaination: "",
  };
  let option = { value: "", isCorrect: false };
  function addNewOption() {
    console.log('option', option)
    question.options = [...question.options, { ...option }];
    // console.log('question.options', question.options)
    cleaOption();
  }
  function addNewQuestion() {
    console.log("question", question);
    questions = [...questions, { ...question }];
    console.log("questions", questions);
    cleaQuestion();
  }
  function cleaOption() {
    option.value = "";
    option.isCorrect = false;
  }
  function cleaQuestion() {
    question.label = "";
    question.options = [];
    question.explaination = "";
  }

  function delQuestion(question) {
    console.log("qu", question);
    questions = questions.filter((q) => q !== question);
  }

  function editQuestion(question) {
    console.log("item", question);
  }

  function onSelectedquestion(question) {
    console.log("question", question);
  }
</script>

<svelte:head>
  <title>Quiz Panel</title>
  <meta name="description" content=" Quiz Panel app" />
</svelte:head>

<div>
  <h1>Quiz Panel</h1>

  <div>
    <h2>Question</h2>
    <input type="text" bind:value={question.label} />
    <br />
    <h2>Explaination</h2>
    <input type="text" bind:value={question.explaination} />
    <br />
    <h2>Options</h2>
    <div>
      <input type="checkbox" bind:checked={option.isCorrect} />
      <input type="text" bind:value={option.value} />
      <button
      class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 text-center mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
      on:click={addNewOption}>Add Option</button
      >
    </div>
    <br />
    <div>
      {#each question.options as option}
        <div>
          <input type="checkbox" bind:checked={option.isCorrect} />
          <input type="text" bind:value={option.value} />
        </div>
      {/each}
    </div>
    <br />
    <button
      class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 text-center mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
      on:click={addNewQuestion}>Add Question</button
    >
  </div>

  <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
    <thead
      class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400"
    >
      <tr>
        <th scope="col" class="py-3 px-6">Question</th>
        <th scope="col" class="py-3 px-6">Options</th>
        <th scope="col" class="py-3 px-6">Explaination</th>
        <th scope="col" class="py-3 px-6">Actions</th>
      </tr>
    </thead>
    <tbody>
        <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
          <td class="py-4 px-6" contenteditable="true">{question.label}</td>
          <div>
            {#each question.options as option}
              <td>
                {option.value}
              </td>
              <td class="py-4 px-6">{option.isCorrect}</td>
            {/each}
          </div>
          <td class="py-4 px-6" contenteditable="true"
            >{question.explaination}</td
          >
          <td class="py-4 px-6">
            <br />
            <button
            class="text-white bg-blue-700 hover:bg-blue-800 focus:outline-none focus:ring-4 focus:ring-blue-300 font-medium rounded-full text-sm px-5 py-2.5 text-center mr-2 mb-2 dark:bg-blue-600 dark:hover:bg-blue-700 dark:focus:ring-blue-800"
            on:click={delQuestion(question)}>Delete Question</button
            >
          </td>
        </tr>
    </tbody>
  </table>
</div>

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

  body > table {
    width: 80%;
  }

  table {
    border-collapse: collapse;
  }
  table.list {
    width: 100%;
  }

  td,
  th {
    border: 1px solid #dddddd;
    text-align: left;
    padding: 8px;
  }
  tr:nth-child(even),
  table.list thead > tr {
    background-color: #dddddd;
  }

  input[type="text"],
  input[type="number"] {
    width: 100%;
    padding: 8px 20px;
    margin: 8px 0;
    display: inline-block;
    border: 1px solid #ccc;
    border-radius: 4px;
    box-sizing: border-box;
  }

  input[type="submit"] {
    width: 30%;
    background-color: black;
    color: white;
    padding: 10px 18px;
    /* margin: 0px 0; */
    border: none;
    border-radius: 5px;
    cursor: pointer;
  }

  form div.form-action-buttons {
    text-align: right;
  }

  a {
    cursor: pointer;
    text-decoration: underline;
    color: #0000ee;
    margin-right: 4px;
  }

  label.validation-error {
    color: red;
    margin-left: 5px;
  }

  .hide {
    display: none;
  }
</style>
