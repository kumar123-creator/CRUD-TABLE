<script>
	export let teams = []
  
	let newTeam = {
	  rank:'',
	  name: '',
	  matches: '',
	  won: '',
	  lost: '',
	  points: '',
	};
  
	let editTeam = {
      rank:'',
	  name: '',
	  matches: '',
	  won: '',
	  lost: '',
	  points: '',
	};
  
	function addTeam() {
	  teams = [...teams, newTeam];
	  newTeam = {
		rank:'',
		name: '',
		matches: '',
		won: '',
		lost: '',
		points: '',
	  };
	}
  
	function edit(index) {
	  editTeam = {...teams[index]};
	  teams.splice(index, 1);
	}
  
	function updateTeam() {
	  teams = [...teams, editTeam];
	  editTeam = {
		rank:'',
		name: '',
		matches: '',
		won: '',
		lost: '',
		points: '',
	  };
	}
  
	function deleteTeam(index) {
	  teams.splice(index, 1);
	}
  </script>
  
  <style>
	table, th, td {
	  border: 1px solid black;
	  padding: 10px;
	}
  </style>
  
  <table>
	<thead>
	  <tr>
		<th>Rank</th>
		<th>Team Name</th>
		<th>Matches</th>
		<th>Won</th>
		<th>Lost</th>
		<th>Points</th>
		<th>Actions</th>
	  </tr>
	</thead>
	<tbody>
	  {#each teams as team, index}
		<tr>
		  <td>{team.rank}</td>
		  <td>{team.name}</td>
		  <td>{team.matches}</td>
		  <td>{team.won}</td>
		  <td>{team.lost}</td>
		  <td>{team.points}</td>
		  <td>
			<button on:click={() => edit(index)}>Edit</button>
			<button on:click={() => deleteTeam(index)}>Delete</button>
		  </td>
		</tr>
	  {/each}
	  <tr>
		<td><input type="text" bind:value={newTeam.rank}></td>
		<td><input type="text" bind:value={newTeam.name}></td>
		<td><input type="text" bind:value={newTeam.matches}></td>
		<td><input type="text" bind:value={newTeam.won}></td>
		<td><input type="text" bind:value={newTeam.lost}></td>
		<td><input type="text" bind:value={newTeam.points}></td>
		<td><button on:click={addTeam}>Add</button></td>
	  </tr>
	  <tr>
		<td><input type="text" bind:value={editTeam.rank}></td>
		<td><input type="text" bind:value={editTeam.name}></td>
		<td><input type="text" bind:value={editTeam.matches}></td>
		<td><input type="text" bind:value={editTeam.won}></td>
		<td><input type="text" bind:value={editTeam.lost}></td>
		<td><input type="text" bind:value={editTeam.points}></td>
		<td><button on:click={updateTeam}>Save</button></td>
	  </tr>
	</tbody>
  </table>
  
  
  
