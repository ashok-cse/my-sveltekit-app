<script>

  import { onMount } from 'svelte';
  
  let quizdata = [];

  let options = [];
  
  let currentQuestion = 0;
  let submited = false;
  
  let tick = 59;
  let timer = setInterval(() => {
      tick = tick - 1;
      if(tick == 0){
        clearInterval(timer);
        submited = true;
      }
  }, 1000);
  
  
  async function loadQuiz() {
      const res = await fetch(`https://quiz-panel-server.herokuapp.com/todos`);
      const data = await res.json();
      const quizdata = data.data.quiz[currentQuestion];
      return quizdata;    
    
  }

  

  async function checkAnswer(){
      const selectedOption = document.querySelector('input[name="option"]:checked');
      const selectedValue = selectedOption.value;
      console.log(selectedValue);
      if(selectedValue == quizdata.answer[0].value){
          alert('Correct Answer');
      }else{
          alert('Wrong Answer');
      }
  }

 

  onMount(async () => {
      quizdata = await loadQuiz();
      options = quizdata.options;
  });
  
  async function nextQuestion(){
      currentQuestion = currentQuestion + 1;
      quizdata = await loadQuiz();
      options = quizdata.options;
      tick = 59;
  }
  

  </script>

<svelte:head>
  <title>Start Quiz</title>
  <meta name="description" content="Start a quiz" />
</svelte:head>



<div class="w-full">
 
  <div class="border-r border-b border-l border-gray-400 lg:border-l-0 lg:border-t lg:border-gray-400 bg-white rounded-b lg:rounded-b-none lg:rounded-r p-4 flex flex-col justify-between leading-normal">
  
      <div class="w-full">
  <h1>Answer This Question</h1>
  <h1>00:00:{tick} Seconds Left</h1>
        <div class="w-full bg-slate-700 rounded pt-4 pr-4 pl-4 pb-4 mb-4">
      
          <p class=" text-white text-xl">{quizdata.question}</p>
        </div>
        {#each options as option}
        <div class="w-full flex-auto bg-slate-700 rounded pt-4 pr-4 pl-4 pb-4 mb-4">
          <input type="radio" name="option" id="option" value="{option.value}">
          <p class=" text-white text-xl">{option.value}</p>
        </div>
        {/each}

        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" disabled={submited} on:click={checkAnswer}>
          Submit
        </button>
        <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click={nextQuestion}>
          Next
        </button>
      </div>
  </div>
</div>







