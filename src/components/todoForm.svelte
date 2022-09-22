<script>
  export let addTodo
  let todo = ''

  const handleSubmit = () => {
    addTodo(todo)
    todo = ''
  }
</script>

<form on:submit|preventDefault={handleSubmit}>
  <input
    type="text"
    placeholder="Type here…"
    bind:value={todo}
    class="input input-bordered input-primary w-full"
  />
  <button
    class:btn-disabled={todo === ''}
    type="submit"
    class="btn btn-block mt-4"
  >
    Add
  </button>
</form>
