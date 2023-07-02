<script>
  export let todo;
  export let addTodo;
  export let todoError;
</script>

<section class="flex justify-center w-2/3 mx-auto mt-5">
  <div class="w-2/3">
    <input placeholder="Let's write a todo!" bind:value={todo} class="w-full p-2 bg-teal-100 rounded-md outline-0 placeholder:text-gray-600">
    <p class="mt-1 text-sm text-red-400">
    {todoError}
  </p>
  </div>
  <button on:click={addTodo} class="w-1/5 p-2 ml-2 text-white transition-all bg-teal-500 rounded-md outline-0 active:scale-90 h-fit">Add</button>
</section>
