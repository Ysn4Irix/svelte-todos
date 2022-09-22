<script>
  import Layout from './Layout.svelte'
  import TodoForm from './components/todoForm.svelte'

  let todos = localStorage.getItem('todos')
    ? JSON.parse(localStorage.getItem('todos'))
    : []

  const addTodo = (todo) => {
    todos = [
      ...todos,
      {
        id: Date.now(),
        text: todo,
        done: false,
      },
    ]
  }

  const removeTodo = (id) => {
    todos = todos.filter((todo) => todo.id !== id)
  }

  $: localStorage.setItem('todos', JSON.stringify(todos))
</script>

<Layout>
  <main class="hero mt-5">
    <div class="card card-compact bg-base-100 shadow-xl">
      <div class="card-body items-center text-center">
        <h2 class="card-title pb-2 font-semibold">Svelte todos</h2>
        <div class="form-control">
          <TodoForm {addTodo} />
          <div class="mt-2">
            {#each todos as { id, text, done }, index}
              <div
                class="flex flex-row justify-between items-center text-center"
                {index}
              >
                <input
                  on:click={() => (done = !done)}
                  checked={done}
                  type="checkbox"
                  class="checkbox checkbox-md mr-2"
                />
                <span
                  class={`bg-base-200 shadow-sm rounded-lg my-2 py-3 px-5 font-semibold
                  ${
                    done
                      ? 'line-through bg-accent transition-all duration-200 ease-in-out'
                      : ''
                  }`}
                >
                  {text}
                </span>
                <span
                  class="cursor-pointer ml-1 hover:opacity-50 transition-all duration-300 ease-in-out"
                  on:click={() => removeTodo(id)}
                >
                  <svg
                    width="24"
                    height="24"
                    viewBox="0 0 24 24"
                    style="fill: rgba(248, 114, 114, 1);"
                  >
                    <path
                      d="M6 7H5v13a2 2 0 0 0 2 2h10a2 2 0 0 0 2-2V7H6zm10.618-3L15 2H9L7.382 4H3v2h18V4z"
                    />
                  </svg>
                </span>
              </div>
            {/each}
          </div>
        </div>
      </div>
    </div>
  </main>
</Layout>
