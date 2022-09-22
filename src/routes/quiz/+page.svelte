
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>


<script>
   var selectedRow = null

function onFormSubmit() {
    if (validate()) {
        var formData = readFormData();
        if (selectedRow == null)
            insertNewRecord(formData);
        else
            updateRecord(formData);
        resetForm();
    }
}

function readFormData() {
    var formData = {};
    formData["ques"] = document.getElementById("ques").value;
    formData["myCheck"] = document.getElementById("myCheck").value;
    formData["myCheck1"] = document.getElementById("myCheck1").value;
    formData["myCheck2"] = document.getElementById("myCheck2").value;
    formData["myCheck3"] = document.getElementById("myCheck3").value;
    formData["Options1"] = document.getElementById("Options1").value;
    formData["Options2"] = document.getElementById("Options2").value;
    formData["Options3"] = document.getElementById("Options3").value;
    formData["Options4"] = document.getElementById("Options4").value;
    formData["explain"] = document.getElementById("explain").value;
    return formData;
}

function insertNewRecord(data) {
    var table = document.getElementById("QuesList").getElementsByTagName('tbody')[0];
    var newRow = table.insertRow(table.length);
    cell1 = newRow.insertCell(0);
    cell1.innerHTML = data.ques;
    cell2 = newRow.insertCell(1);
    cell2.innerHTML = data.Options1;
    cell3 = newRow.insertCell(2);
    cell3.innerHTML = data.Options2;
    cell4 = newRow.insertCell(3);
    cell4.innerHTML = data.Options3;
    cell5 = newRow.insertCell(4);
    cell5.innerHTML = data.Options4;
    

    if (document.getElementById("myCheck").checked == true) {
        document.getElementById("myCheck1").checked = false;
        document.getElementById("myCheck2").checked = false;
        document.getElementById("myCheck3").checked = false;
        cell6 = newRow.insertCell(5);
        cell6.innerHTML = data.Options1;
    } if (document.getElementById("myCheck1").checked == true) {
        document.getElementById("myCheck").checked = false;
        document.getElementById("myCheck2").checked = false;
        document.getElementById("myCheck3").checked = false;
        cell6 = newRow.insertCell(5);
        cell6.innerHTML = data.Options2;
    }  if (document.getElementById("myCheck2").checked == true) {
        document.getElementById("myCheck").checked = false;
        document.getElementById("myCheck1").checked = false;
        document.getElementById("myCheck3").checked = false;
        cell6 = newRow.insertCell(5);
        cell6.innerHTML = data.Options3;

    }  if (document.getElementById("myCheck3").checked == true) {
        document.getElementById("myCheck").checked = false;
        document.getElementById("myCheck1").checked = false;
        document.getElementById("myCheck2").checked = false;
        cell6 = newRow.insertCell(5);
        cell6.innerHTML = data.Options4;
    }
    cell7 = newRow.insertCell(6);
    cell7.innerHTML = data.explain;
    cell8 = newRow.insertCell(7);
    cell8.innerHTML = `<a onClick="onEdit(this)">Edit</a>
                       <a onClick="onDelete(this)">Delete</a>`;
}

function resetForm() {
    document.getElementById("ques").value = "";
    document.getElementById("Options1").value = "";
    document.getElementById("Options2").value = "";
    document.getElementById("Options3").value = "";
    document.getElementById("Options4").value = "";
    document.getElementById("answer").value = "";
    document.getElementById("explain").value = "";
    selectedRow = null;
}

function onEdit(td) {
    selectedRow = td.parentElement.parentElement;
    document.getElementById("ques").value = selectedRow.cells[0].innerHTML;
    document.getElementById("Options1").value = selectedRow.cells[1].innerHTML;
    document.getElementById("Options2").value = selectedRow.cells[2].innerHTML;
    document.getElementById("Options3").value = selectedRow.cells[3].innerHTML;
    document.getElementById("Options4").value = selectedRow.cells[4].innerHTML;
    document.getElementById("explain").value = selectedRow.cells[6].innerHTML;
}
function updateRecord(formData) {
    selectedRow.cells[0].innerHTML = formData.ques;
    selectedRow.cells[1].innerHTML = formData.Options1;
    selectedRow.cells[2].innerHTML = formData.Options2;
    selectedRow.cells[3].innerHTML = formData.Options3;
    selectedRow.cells[4].innerHTML = formData.Options4;
    if (document.getElementById("myCheck").checked == true) {
        document.getElementById("myCheck1").checked = false;
        document.getElementById("myCheck2").checked = false;
        document.getElementById("myCheck3").checked = false;
        selectedRow.cells[5].innerHTML = formData.Options1;
    } if (document.getElementById("myCheck1").checked == true) {
        document.getElementById("myCheck").checked = false;
        document.getElementById("myCheck2").checked = false;
        document.getElementById("myCheck3").checked = false;
        selectedRow.cells[5].innerHTML = formData.Options2;
    }  if (document.getElementById("myCheck2").checked == true) {
        document.getElementById("myCheck").checked = false;
        document.getElementById("myCheck1").checked = false;
        document.getElementById("myCheck3").checked = false;
        selectedRow.cells[5].innerHTML = formData.Options3;
    }  if (document.getElementById("myCheck3").checked == true) {
        document.getElementById("myCheck").checked = false;
        document.getElementById("myCheck1").checked = false;
        document.getElementById("myCheck2").checked = false;
        selectedRow.cells[5].innerHTML = formData.Options4;
    }
    selectedRow.cells[6].innerHTML = formData.explain;
}

function onDelete(td) {
    if (confirm('Are you sure to delete this record ?')) {
        row = td.parentElement.parentElement;
        document.getElementById("quesList").deleteRow(row.rowIndex);
        resetForm();
    }
}
function validate() {
    isValid = true;
    checked = false;
    if (document.getElementById("ques").value == "") {
        isValid = false;
        document.getElementById("quesValidationError").classList.remove("hide");
    } else {
        isValid = true;
        if (!document.getElementById("quesValidationError").classList.contains("hide"))
            document.getElementById("quesValidationError").classList.add("hide");
    }
    if (document.getElementById("Options1").checked == false && document.getElementById("Options2").checked == false && document.getElementById("Options3").checked == false && document.getElementById("Options4").checked == false) {
        checked = false;
        console.error("Please Check One Option");
    } else {
        checked = true;
    }
    return isValid;
}    

  </script>
  
 <hr>
			<div class="quiz-form">
                <form onsubmit="event.preventDefault();onFormSubmit();" autocomplete="off">
                    <div>
                        <label>Question</label><label class="validation-error hide" id="quesValidationError">This field is required.</label>
                        <input type="text" name="ques" id="ques">
                    </div>
                    <div>
                        <label>Options1</label>
                        <input type="checkbox" id="myCheck">
                        <input type="text" name="Options1" id="Options1">
                        <label>Options2</label>
                        <input type="checkbox" id="myCheck1">
                        <input type="text" name="Options2" id="Options2">
                        <label>Options3</label>
                        <input type="checkbox" id="myCheck2">
                        <input type="text" name="Options3" id="Options3">
                        <label>Options4</label>
                        <input type="checkbox" id="myCheck3">
                        <input type="text" name="Options4" id="Options4">  
                    </div>
                    <div>
                        <label>Explain Ans</label>
                        <input type="text" name="explain" id="explain">
                    </div>
                    <div  class="form-action-buttons">
                        <input type="submit" value="Submit">
                    </div>
                </form>
		</div>
		<br/>
		<div class = "quiz-table">
                <table class="list" id="QuesList">
                    <thead>
                        <tr>
                            <th>Question</th>
                            <th>Options1</th>
                            <th>Options2</th>
                            <th>Options3</th>
                            <th>Options4</th>
                            <th>Correct Ans</th>
                            <th>Explain</th>
                            <th>Actions</th>
                        </tr>
                    </thead>
                    <tbody>

                    </tbody>
                </table>
        </div>

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


