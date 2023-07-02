<script>
  import {Icon, Trash, Check, XMark, PencilSquare, ArrowRightCircle} from 'svelte-hero-icons';

  export let todoList;
  export let deleteTodo;
  export let handleCompleteTodo;
  export let handleEditTodo;
  export let handleUpdateTodo;
  export let editedTodo;
</script>

{#if (todoList?.length > 0)}
  <div class="w-2/3 h-screen mx-auto mt-10">
    {#each todoList as todo (todo?.id)}
    <section class="flex items-center justify-between px-4 py-2 mb-4 rounded bg-teal-50">
      <div class="flex items-center gap-4">
        {#if (todo?.isEditing)}
          <input bind:value={editedTodo} type="text" class="p-2 bg-white">
        {:else}
          <p class={`text-lg font-regular ${todo?.isCompleted ? 'text-decoration-line: line-through' : ''}`}>{todo?.todo}</p>
        {/if}
      </div>
      {#if todo?.isEditing}
        <button on:click={() => handleUpdateTodo(todo.id)} class="active:scale-90 outline-1">  
          <Icon solid mini src={ArrowRightCircle} class='w-5 h-5 text-yellow-500'/>
        </button>
      {:else} 
        <div class="flex items-center gap-2">
        {#if (todo?.isCompleted)}
          <button on:click={() => handleCompleteTodo(todo?.id)}   class="active:scale-90 outline-1">  
            <Icon solid mini src={XMark} class='w-5 h-5 text-red-300'/>
          </button>
        {:else}
          <button on:click={() => handleCompleteTodo(todo?.id)}   class="active:scale-90 outline-1">  
            <Icon solid mini src={Check} class='w-5 h-5 text-green-300'/>
          </button>
        {/if}
        <button on:click={() => handleEditTodo(todo?.id)}   class="active:scale-90 outline-1">  
            <Icon solid mini src={PencilSquare} class='w-5 h-5 text-yellow-500'/>
          </button>
        <button on:click={() => deleteTodo(todo?.id)} class="active:scale-90 outline-1">
          <Icon solid mini src={Trash} class='w-5 h-5 text-red-300'/>
        </button>
      </div>
      {/if}
    </section>
    {/each}
  </div>
{/if}