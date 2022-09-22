
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>


<script>
    let quizQuestion = "";
    let quizAnswer = "";
    let quizOptions = [""];
    let quizOptionsCount = 0;
    let quizOptionsCountMax = 100;
    let quizOptionsCountMin = 2;

    function addOption() {
        if (quizOptionsCount < quizOptionsCountMax) {
            quizOptionsCount++;
            quizOptions.push("");
        }
    }

    function removeOption() {
        if (quizOptionsCount > quizOptionsCountMin) {
            quizOptionsCount--;
            quizOptions.pop();
        }
    }

    function submitQuiz() {
        console.log(quizQuestion);
        console.log(quizAnswer);
        console.log(quizOptions);
    }

    function resetQuiz() {
        quizQuestion = "";
        quizAnswer = "";
        quizOptions = [];
        quizOptionsCount = 0;
    }

    function handleOptionChange(event, index) {
        quizOptions[index] = event.target.value;
    }

    function handleAnswerChange(event) {
        quizAnswer = event.target.value;
    }

    function handleQuestionChange(event) {
        quizQuestion = event.target.value;
    }

    function handleOptionCountChange(event) {
        quizOptionsCount = event.target.value;
    }

    function handleOptionCountSubmit(event) {
        event.preventDefault();
        if (quizOptionsCount > quizOptionsCountMax) {
            quizOptionsCount = quizOptionsCountMax;
        } else if (quizOptionsCount < quizOptionsCountMin) {
            quizOptionsCount = quizOptionsCountMin;
        }
        quizOptions = [];
        for (let i = 0; i < quizOptionsCount; i++) {
            quizOptions.push("");
        }
    }

    function handleOptionCountReset(event) {
        event.preventDefault();
        quizOptionsCount = 0;
        quizOptions = [];
    }

    function handleOptionCountBlur(event) {
        if (quizOptionsCount > quizOptionsCountMax) {
            quizOptionsCount = quizOptionsCountMax;
        } else if (quizOptionsCount < quizOptionsCountMin) {
            quizOptionsCount = quizOptionsCountMin;
        }
    }

    function handleOptionCountFocus(event) {
        event.target.select();
    }

    function handleOptionCountKeyDown(event) {
        if (event.key === "Enter") {
            handleOptionCountSubmit(event);
        }
    }

    function handleOptionCountKeyUp(event) {
        if (event.key === "Escape") {
            handleOptionCountReset(event);
        }
    }

    function handleOptionCountMouseUp(event) {
        event.target.select();
    }

    function handleOptionCountWheel(event) {
        event.preventDefault();
        if (event.deltaY > 0) {
            quizOptionsCount--;
        } else {
            quizOptionsCount++;
        }
        if (quizOptionsCount > quizOptionsCountMax) {
            quizOptionsCount = quizOptionsCountMax;
        } else if (quizOptionsCount < quizOptionsCountMin) {
            quizOptionsCount = quizOptionsCountMin;
        }
    }

    function handleOptionCountPaste(event) {
        event.preventDefault();
        let clipboardData = event.clipboardData || window.clipboardData;
        let pastedData = clipboardData.getData("text");
        if (pastedData) {
            quizOptionsCount = parseInt(pastedData);
        }
    }

    function handleOptionCountCut(event) {
        event.preventDefault();
        let clipboardData = event.clipboardData || window.clipboardData;
        let cutData = quizOptionsCount.toString();
        if (cutData) {
            clipboardData.setData("text", cutData);
            quizOptionsCount = 0;
        }
    }

    function handleOptionCountCopy(event) {
        event.preventDefault();
        let clipboardData = event.clipboardData || window.clipboardData;
        let copyData = quizOptionsCount.toString();
        if (copyData) {
            clipboardData.setData("text", copyData);
        }
    }

    function handleOptionCountSelect(event) {
        event.target.select();
    }

    function handleOptionCountSelectStart(event) {
        event.preventDefault();
    }

    function handleOptionCountSelectEnd(event) {
        event.preventDefault();
    }

    function handleOptionCountSelectAll(event) {
        event.preventDefault();
    }

    function handleOptionCountContextMenu(event) {
        event.preventDefault();
    }

    function handleOptionCountDrag(event) {
        event.preventDefault();
    }

    function handleOptionCountDragStart(event) {
        event.preventDefault();
    }

    function handleOptionCountDragEnd(event) {
        event.preventDefault();
    }

    function handleOptionCountDragEnter(event) {
        event.preventDefault();
    }

    function handleOptionCountDragOver(event) {
        event.preventDefault();
    }

    function handleOptionCountDragLeave(event) {
        event.preventDefault();
    }

    function handleOptionCountDrop(event) {
        event.preventDefault();
        let dataTransfer = event.dataTransfer || event.originalEvent.dataTransfer;
        let droppedData = dataTransfer.getData("text");
        if (droppedData) {
            quizOptionsCount = parseInt(droppedData);
        }
    }
    

  </script>
  
  <div>
    <form on:submit={submitQuiz}>
      <label for='name'>Name</label>
      <input 
        type="text" 
        placeholder="Name of superhero" 
        name="name"
        required 
        bind:value={quizQuestion} 
      />
      <br />
      <label for='weapon'>Weapon</label>
      <input 
        type="text" 
        placeholder="Weapon" 
        name="weapon" 
        required
        bind:value={quizAnswer} 
      />
      <br />
      <label for='team'>Team</label>
      <select 
        name="team" 
        required
        bind:value={quizOptions} 
      >
        <option value={'Avengers'}>Avengers</option>
        <option value={'Justice League'}>Justice League</option>
        <option value={'X-Men'}>X-Men</option>
      </select>
      <br /><br />
      <input type="submit" />
    </form>
  </div>
  <hr />
  <table>
    <thead>
      <tr>
        <th>Name</th>
        <th>Weapon</th>
        <th>Team</th>
      </tr>
    </thead>
    <tbody>
      <tr>
        <td>{quizQuestion}</td>
        <td>{quizAnswer}</td>
        <td>{quizOptions}</td>
        log: {JSON.stringify(quizOptions)}
        log: {JSON.stringify(quizOptions[0])}
        log: {JSON.stringify(quizOptions[1])}
        log: {JSON.stringify(quizOptions[2])}
        
      </tr>
    </tbody>
    </table>


<style>
	* {
		font-family: inherit;
		font-size: inherit;
	}

	input {
		display: block;
		margin: 0 0 0.5em 0;
	}

	select {
		float: left;
		margin: 0 1em 1em 0;
		width: 14em;
	}

	.buttons {
		clear: both;
	}
</style>


