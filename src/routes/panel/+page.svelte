<script>
 
 import { onMount } from "svelte";

  let quizdata = [];
  let question = "";
  let answer = [];
  let options = [];
  let exlpain = "";
  let option = { value: "", isCorrect: false };

  let correctOption = { value: ""};

  async function addOption() {
    options = [...options, { ...option }];
   
    if(option.isCorrect == true){
        answer = [...answer, { ...option }];
    }
    console.log('Correctoptions', answer);
    console.log(options);
  }

  async function createQuiz() {

    const res = await fetch(`https://quiz-panel-server.herokuapp.com/todos/create`, {
      method: "POST",
      headers: {
        "Content-Type": "application/json",
      },
      body: JSON.stringify({
        question: question,
        answer: answer,
        options: options,
        explain: exlpain,
      }),
    }).then((res) => {
      res.json();
    });

    window.location.href = "/panel";
  }

    async function loadQuiz() {
    const res = await fetch(`https://quiz-panel-server.herokuapp.com/todos`);
    const data = await res.json();
    const quizdata = data.data.quiz;
    return quizdata;
}

  onMount(async () => {
    quizdata = await loadQuiz();
  });

</script>

<svelte:head>
  <title>Panel</title>
  <meta name="description" content="Panel app" />
</svelte:head>

<div class="w-full bg-white shadow-md rounded px-8 pt-6 pb-8 mb-4">
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="question">
        Enter Full Question
      </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 leading-tight focus:outline-none focus:shadow-outline"
        bind:value={question}
        type="text"
        placeholder="Enter full question here"
      />
    </div>

    <div class="mb-4">
        <label class="block text-gray-700 text-sm font-bold mb-2" for="answer">
          Write Explanation
        </label>
        <input
          class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
          bind:value={exlpain}
          type="text"
          placeholder="correct explanation"
        />
      </div>
    <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="options">
        Enter Option Value
      </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
        bind:value={option.value}
        type="text"
        placeholder="option value"
      />
      <input class="mr-2 leading-tight" type="checkbox" bind:checked={option.isCorrect}/>
      <span class="text-sm"> Is this correct option? </span>
    </div>
   
    <div class="flex items-center justify-between">
      <button
        class="bg-blue-500  hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline"
        on:click={addOption}
        type="submit"
      >
        Add Option
      </button>
    </div>
</div>
<div class="w-full">



    <h1>Total No. Options</h1>

    <div class="border-r border-b border-l border-gray-400 lg:border-l-0 lg:border-t lg:border-gray-400 bg-white rounded-b lg:rounded-b-none lg:rounded-r p-4 flex flex-col justify-between leading-normal">
    
        <div class="w-full">
    
            {#each options as option}
          
        <div class="w-full bg-slate-700 rounded pt-4 pr-4 pl-4 pb-4 mb-4">

            <p class=" text-white text-xl">{option.value}</p>
        </div>
            {/each}
        </div>

        <div class="flex items-center justify-between">
           <button  class="bg-blue-500  hover:bg-blue-700 text-white font-bold py-2 px-4 rounded focus:outline-none focus:shadow-outline" on:click={createQuiz}>
         Add Question   
        </button>
           
          </div>
     
    </div>



  </div>


<!-- List of Questions -->


<div class="w-full">



    <h1>Total No. Questions</h1>
     
<!-- <div class="overflow-x-auto relative shadow-md sm:rounded-lg">
    <table class="w-full text-sm text-left text-gray-500 dark:text-gray-400">
        <thead class="text-xs text-gray-700 uppercase bg-gray-50 dark:bg-gray-700 dark:text-gray-400">
            <tr>
                <th scope="col" class="py-3 px-6">
                    Question
                </th>

                <th scope="col" class="py-3 px-6">
                    Options
                </th>

                <th scope="col" class="py-3 px-6">
                    Answer
                </th>
                <th scope="col" class="py-3 px-6">
                    Explain
                </th>
            </tr>
        </thead>

        {#each quizdata as quiz}
        <tbody>
            <tr class="bg-white border-b dark:bg-gray-800 dark:border-gray-700">
                <td class="py-4 px-6">
                    {quiz.question}
                </td>
                <td class="py-4 px-6">
                    {#each quiz.options as option}
                    <ul class=" list-disc">
                        <li>{option.value}</li>
                    </ul>
                    {/each}
                </td>
                <td class="py-4 px-6">
                    {quiz.answer[0].value}
                </td>
                <td class="py-4 px-6">
                    {quiz.explain}
                </td>
            </tr>
        </tbody>
        {/each}
    </table>
</div>
</div> -->

</div>


