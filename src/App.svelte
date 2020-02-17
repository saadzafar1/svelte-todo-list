<script>
  import Header from './components/Header.svelte';
  import List from './components/List.svelte';

  let task = '';
  let taskList = [];

  const addListItem = () => {
    if(task === "") return;
    const updatedList = [...taskList];
    updatedList.push({
      text: task,
      isCompleted: false
    });
    taskList = updatedList;
    task = '';
  }

  const updateListStatus = (event) => {
    const updatedList = [...taskList];
    const index = event.detail;
    updatedList[index].isCompleted = !updatedList[index].isCompleted;
    taskList = updatedList;
  }
  
  const updateList = event => {
    const updatedList = [...taskList];
    const index = event.detail;
    updatedList.splice(index,1);
    taskList = updatedList;
  }
</script>

<main>
  <Header />
  <form on:submit|preventDefault={addListItem}>
    <input type="text" placeholder="Enter task description" bind:value={task} class="task-field">
    <button type="submit" class="btn">Add Task</button>
  </form>
  <List on:completeTask={updateListStatus} on:removeTask="{updateList}" list={taskList}/>
</main>

<style>
  :root {
    --color-primary: #ff3e00;
  }
  main {
    text-align: center;
    padding: 1em;
    max-width: 540px;
    margin: 0 auto;
  }

  h1 {
    color: #ff3e00;
    text-transform: uppercase;
    font-size: 4em;
    font-weight: 100;
  }
  .task-field {
    border: 1px solid #ccc;
    outline: none;
    padding: 10px;
    transition: all 0.2s ease;
    border-radius: 2px;
    width: 80%;
  }
  .task-field:focus {
    border-color: var(--color-primary);
  }
  .btn {
    background-color: transparent;
    padding: 10px;
    border: 1px solid var(--color-primary);
    color: var(--color-primary);
    transition: all 0.2s ease;
    cursor: pointer;
    border-radius: 2px;
    position: relative;
    outline: none;
  }
  .btn::before {
    content: "";
    height: 100%;
    width: 100%;
    position: absolute;
    top: 0;
    left: 0;
    transform: scaleX(0);
    transform-origin: 0%;
    transition: all 0.2s ease;
    background-color: var(--color-primary);
  z-index: -1;
  }
  .btn:hover::before {
    transform: scaleX(1);
  }
  .btn:hover {
    color: #fff;
  }

  @media screen and (max-width: 568px) {
    .task-field{
      width: 50%;
      margin-top: 10px;
    }
  }
</style>
