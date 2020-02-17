<script>
  import { createEventDispatcher } from 'svelte';

  const dispatch = createEventDispatcher();
  const setIsCompleted = index => {
    dispatch('completeTask', index);
  };
  const onDelete = index => {
    dispatch('removeTask', index);
  };
  export let list;
</script>
<div class="list-container">
  {#if list.length > 0}
  <ul>
    {#each list as item,i}
    <li>
      <div class="item-container">
        <span
          class="{item.isCompleted ? 'item-text completed' : 'item-text'}"
          on:click|preventDefault="{setIsCompleted.bind(this,i)}"
          >{item.text}</span
        >
        <span class="delete-btn" on:click="{onDelete.bind(this,i)}">
          <i class="fa fa-trash-alt"></i>
        </span>
      </div>
    </li>
    {/each}
  </ul>
  {:else}
  <div class="message">Woohoo! No tasks for today</div>
  {/if}
</div>
<style>
  .message {
    margin-top: 10px;
  }
  .list-container ul {
    padding: 0;
    list-style: none;
    background-color: #fff;
    box-shadow: 0 2px 5px rgba(0, 0, 0, 0.1);
  }
  .list-container ul li:nth-child(even) {
    background-color: #eee;
  }
  .list-container ul li {
    padding: 10px 20px;
    text-align: left;
  }
  .list-container ul li .item-container {
    display: flex;
    justify-content: space-between;
    align-items: center;
  }
  .list-container ul li .item-container .item-text {
    flex: 1;
    cursor: pointer;
  }
  .list-container ul li .item-container .item-text.completed {
    text-decoration: line-through;
  }
  .list-container ul li .delete-btn {
    color: #ff3e00;
    cursor: pointer;
  }
</style>
