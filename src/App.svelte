
<script>
	let tasks = [
	  { id: 1, title: "Task 1", stage: 1 },
	  { id: 2, title: "Task 2", stage: 1 },
	  { id: 3, title: "Task 3", stage: 2 },
	  { id: 4, title: "Task 4", stage: 3 }
	];
  
	let newTaskTitle = "";
  
	function addTask() {
	  const newTask = {
		id: Math.max(...tasks.map(t => t.id)) + 1,
		title: newTaskTitle,
		stage: 1
	  };
	  tasks = [...tasks, newTask];
	  newTaskTitle = "";
	}
  
	function editTask(task) {
	  const index = tasks.findIndex(t => t.id === task.id);
	  tasks[index] = task;
	}
  
	function deleteTask(task) {
	  tasks = tasks.filter(t => t.id !== task.id);
	}
  
	function handleDragStart(event, task) {
	  event.dataTransfer.setData("text/plain", task.id);
	}
  
	function handleDragOver(event) {
	  event.preventDefault();
	}
  
	function handleDrop(event, stage) {
	  const taskId = event.dataTransfer.getData("text/plain");
	  const task = tasks.find(t => t.id == taskId);
	  if (task) {
		const index = tasks.findIndex(t => t.id == task.id);
		tasks[index].stage = stage;
		tasks = [...tasks];
	  }
	}
  </script>
  
  <div>
	<h2>Task Pipeline</h2>
	<div>
	  <h3>To Do</h3>
	  <ul on:drop={(event) => handleDrop(event, 1)} on:dragover={handleDragOver}>
		{#each tasks.filter(t => t.stage === 1) as task}
		  <li draggable={true} on:dragstart={(event) => handleDragStart(event, task)}>
			<div>
			  <span>{task.title}</span>
			  <button on:click={() => deleteTask(task)}>Delete</button>
			  <button on:click={() => editTask(task)}>Edit</button>
			</div>
		  </li>
		{/each}
	  </ul>
	</div>
	<div>
	</div>
	  <h3>In Progress</h3>
	  <ul on:drop={(event) => handleDrop(event, 2)} on:dragover={handleDragOver}>
		{#each tasks.filter(t => t.stage === 2) as task}
		  <li draggable={true} on:dragstart={(event) => handleDragStart(event, task)}>
			<div>
			  <span>{task.title}</span>
			  <button on:click={() => deleteTask(task)}>Delete</button>
			  <button on:click={() => editTask(task)}>Edit</button>
			</div>
		  </li>
		{/each}
	  </ul>
	</div>
	<div>
	  <h3>Done</h3>
	  <ul on:drop={(event) => handleDrop(event, 3)} on:dragover={handleDragOver}>
		{#each tasks.filter(t => t.stage === 3) as task}
		  <li draggable={true} on:dragstart={(event) => handleDragStart(event, task)}>
			<div>
			  <span>{task.title}</span>
			  <button on:click={() => deleteTask(task)}>Delete</button>
			  <button on:click={() => editTask(task)}>Edit</button>
			</div>
		  </li>
		{/each}
	  </ul>
	</div>
  
