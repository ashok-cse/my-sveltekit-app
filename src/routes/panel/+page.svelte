<script>
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
      console.log(res);
    });

  }
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
    <!-- <div class="mb-4">
      <label class="block text-gray-700 text-sm font-bold mb-2" for="answer">
        Enter Correct Answer
      </label>
      <input
        class="shadow appearance-none border rounded w-full py-2 px-3 text-gray-700 mb-3 leading-tight focus:outline-none focus:shadow-outline"
        bind:value={answer}
        type="text"
        placeholder="correct answer"
      />
    </div> -->
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
        type="button"
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
            </button>
           
          </div>
     
    </div>

  </div>
