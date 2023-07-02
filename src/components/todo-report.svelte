<script>
  export let totalTodo, totalCompletedTodo, totalIncompleteTodo;
</script>

<section class="w-1/5 p-4 mt-5 shadow xl:fixed right-10 top-20">
  <div>
    <h2 class="text-2xl font-semibold text-center text-teal-600">
      Report
    </h2>
    <article>
      {#if (totalTodo > 0)}
      <table class="table w-full mt-2 table-fixed">
        <thead class="table-header-group">
          <tr>
            <th>Total {totalTodo > 1 ? 'todos' : 'todo'}</th>
            <th>Completed</th>
            <th>Incompleted</th>
          </tr>
        </thead>
        <tbody>
          <tr class="text-center">
            <td>{totalTodo}</td>
            <td>{totalCompletedTodo}</td>
            <td>{totalIncompleteTodo}</td>
          </tr>
        </tbody>
      </table>
      {:else}
      <p class="mt-4 text-base font-semibold text-center">
        Create todos to generate report!
      </p>
      {/if}
    </article>
  </div>
</section>