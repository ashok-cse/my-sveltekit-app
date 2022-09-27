<script>

  import { onMount } from 'svelte';
  
  let quizdata = [];
  let quizdataid = [];

  let question = "";
  let answer = [];
  let options = [];
  let explain = "";
  let option = { value: "", isCorrect: false };

  
  async function loadQuiz() {
      const res = await fetch(`https://quiz-panel-server.herokuapp.com/todos`);
      const data = await res.json();
      const quizdata = data.data.quiz;
      return quizdata;     
  }

  async function getId() {
      
      const res = await fetch(`https://quiz-panel-server.herokuapp.com/todos/${id}`);
      const data = await res.json();
      const quizdataid = data.data.quiz;
      return quizdataid;     
  }
 
  onMount(async () => {
      quizdata = await loadQuiz();
      quizdataid = await getId();
  });
  

  </script>

<svelte:head>
  <title>Start Quiz</title>
  <meta name="description" content="Start a quiz" />
</svelte:head>



<div class="w-full">

  <h1>Total No. Questions</h1>

  <div class="border-r border-b border-l border-gray-400 lg:border-l-0 lg:border-t lg:border-gray-400 bg-white rounded-b lg:rounded-b-none lg:rounded-r p-4 flex flex-col justify-between leading-normal">
  
      <div class="w-full">
  
          {#each quizdata as quiz}
        
          <a href="/quiz/{quiz._id}"> 
          <div class="w-full bg-slate-700 rounded pt-4 pr-4 pl-4 pb-4 mb-4">
         
          <p class=" text-white text-xl">{quiz.question}</p>
      </div></a>
          {/each}
      </div>
  </div>
</div>



