
<svelte:head>
	<title>Quiz Panel</title>
	<meta name="description" content=" Quiz Panel app" />
</svelte:head>


<script>
    let superheroName = "";
    let superheroWeapon = "";
    let superheroTeam = "";
    let editEntryIndex = -1;
  
    const superhero = [
      {
        name: "Captain America",
        weapon: "Shield",
        team: "Avengers"
      },
      {
        name: "Flash",
        weapon: "Speed",
        team: "Justice League"
      },
      {
        name: "Wolverine",
        weapon: "Claws",
        team: "X-Men"
      }
    ];
  
    function submitForm(e) {
      e.preventDefault();
  
      if (editEntryIndex > -1) {
        superhero[editEntryIndex] = {
          name: superheroName,
          weapon: superheroWeapon,
          team: superheroTeam
        };
      } else {
        superhero.push({
          name: superheroName,
          weapon: superheroWeapon,
          team: superheroTeam
        });
      }
  
      superhero = superhero;
      superheroName = "";
      superheroTeam = "";
      superheroWeapon = "";
      editEntryIndex = -1;
    }
  
    function editSuperhero(index) {
      editEntryIndex = index;
      superheroName = superhero[editEntryIndex].name;
      superheroTeam = superhero[editEntryIndex].team;
      superheroWeapon = superhero[editEntryIndex].weapon;
    }
  
    function deleteSuperhero(index) {
      superhero.splice(index, 1);
      superhero = superhero;
    }
  </script>
  
  <div>
    <form on:submit={submitForm}>
      <label for='name'>Name</label>
      <input 
        type="text" 
        placeholder="Name of superhero" 
        name="name"
        required 
        bind:value={superheroName} 
      />
      <br />
      <label for='weapon'>Weapon</label>
      <input 
        type="text" 
        placeholder="Weapon" 
        name="weapon" 
        required
        bind:value={superheroWeapon} 
      />
      <br />
      <label for='team'>Team</label>
      <select 
        name="team" 
        required
        bind:value={superheroTeam} 
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
      {#each superhero as singlehero, index (index)}
      <tr>
        <td>{singlehero.name}</td>
        <td>{singlehero.weapon}</td>
        <td>{singlehero.team}</td>
        <td>
          <a 
            href="#" 
            on:click={() => editSuperhero(index)}>
            Edit
          </a>
        </td>
        <td>
          <a 
            href="#" 
            on:click={() => deleteSuperhero(index)}>
            Delete
          </a>
        </td>
      </tr>
      {/each}
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


