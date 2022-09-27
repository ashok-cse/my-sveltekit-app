<script>
    import { page } from '$app/stores';
    import { onMount } from 'svelte';

    let id = "";

    let quizdataid = [];
    let options = [];

    let correctOption = { value: ""};

    async function getId() {
        id = $page.params.slug
        const res = await fetch(`https://quiz-panel-server.herokuapp.com/todos/${id}`);
        const data = await res.json();
        const quizdataid = data.data.quiz;
        return quizdataid;     
    }

    async function checkAnswer(){
        const selectedOption = document.querySelector('input[name="option"]:checked');
        const selectedValue = selectedOption.value;
        console.log(selectedValue);
        if(selectedValue == quizdataid.answer[0].value){
            alert('Correct Answer');
            correctOption = { value: selectedValue};
        }else{
            alert('Wrong Answer');
        }
    }
   
    onMount(async () => {
        quizdataid = await getId();

    if(quizdataid.options.length > 0){
        options = quizdataid.options;
    }
      
    });
    
  
    </script>
  
  <svelte:head>
    <title>Answer Quiz</title>
    <meta name="description" content="Start a quiz" />
  </svelte:head>
  
  
  <div class="w-full">

    <h1>Answer Question</h1>

    <div class="border-r border-b border-l border-gray-400 lg:border-l-0 lg:border-t lg:border-gray-400 bg-white rounded-b lg:rounded-b-none lg:rounded-r p-4 flex flex-col justify-between leading-normal">
    
        <div class="w-full">          
            <div class="w-full bg-slate-700 rounded pt-4 pr-4 pl-4 pb-4 mb-4">      
            <p class=" text-white text-xl">{quizdataid.question}</p>
        </div>
       {#each options as option}
         <div class="w-full bg-slate-700 rounded pt-4 pr-4 pl-4 pb-4 mb-4">
            <input type="radio" name="option" id="option" value="{option.value}">
                <p class=" text-white text-xl">{option.value}</p>
          </div>
         {/each}
            <button class="bg-blue-500 hover:bg-blue-700 text-white font-bold py-2 px-4 rounded" on:click={checkAnswer}>
                Submit Answer
            </button>

    </div>
  </div>
 
  </div>

  
  
  
  
  
  