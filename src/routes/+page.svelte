<script>
	let showDoneTask = false;
	let newTaskInput = '';
	let taskList = [
		{ name: 'tache une', done: false },
		{ name: 'tache deux', done: false }
	];
	let doneTaskList = [];

	function addTask() {
		taskList.push({ name: newTaskInput, done: false });
		newTaskInput = '';
		taskList=taskList // Reset the input value after adding a task
	}

	function handleShowDoneTask() {
		showDoneTask = !showDoneTask;
	}

	function validateTask(index) {
		console.log('validate task');
		taskList[index].done = true;
		doneTaskList.push(taskList[index]);
		taskList.splice(index, 1);

		refreshArray();
	}

	function unvalidateTask(index) {
		console.log('unvalidate task');

		doneTaskList[index].done = false;
		taskList.push(doneTaskList[index]);
		doneTaskList.splice(index, 1);

		refreshArray();
	}

	function refreshArray() {
		taskList = taskList;
		doneTaskList = doneTaskList;
	}


</script>
<h1>TO DO IT.</h1>
<form on:submit|preventDefault={addTask}>
	<input type="text" bind:value={newTaskInput} />
	<button>Ok</button>
</form>
<div class="tasklist_container">

<p class="taskdone_question">
	Voir les taches effectuées?<input
		type="checkbox"
		bind:checked={showDoneTask}
		on:click={handleShowDoneTask}
	/>
</p>


	{#if showDoneTask == false}
	{#each taskList as task, index}
	
	<p>
		{task.name}
		<input
		type="checkbox"
		bind:checked={task.done}
		on:click|preventDefault={() => validateTask(index)}
		/>
	</p>
	{/each}
	{:else}
	{#each doneTaskList as doneTask, index}
	{#if showDoneTask === true}
	<p>
		{doneTask.name}<input
		type="checkbox"
		bind:checked={doneTask.done}
		on:click|preventDefault={() => unvalidateTask(index)}
		/>
	</p>
	{/if}
	{/each}
	{/if}
	
</div>

<style>
	h1{
		color: white;
		font-size: 4rem;
		text-align: center;
	}

	form{
		width: 20vw;
		display: flex;
		justify-content: space-between;
		height: 40px;
		border-radius: 30px;
		border: 1px solid white;
		margin-left: auto;
		margin-right: auto;
	}

	form input{
		border: none;
		background-color: transparent;
		height: 100%;
		outline: none;
		font-size: 16px;
		width: 75%;
		padding-left: 20px;
	}

	form button{
		height: 100%;
	    width: 20%;
		border-top-right-radius: 30px;
		border-bottom-right-radius: 30px;
		border: none;
	}

	.tasklist_container{
	 width: 50vw;
	 margin-left: auto;
	 margin-right: auto;
	}

	.taskdone_question{
		text-align: center;
		font-size: 1.5rem;
	}

	input[type="checkbox"]{
		
		height: 20px;
		width: 20px;
		border:1px solid black;
		border-radius: 15px;
		margin-left: 10px;

	}
	</style>