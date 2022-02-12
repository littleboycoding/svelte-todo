<script lang="typescript">
  interface Todo {
    text: string;
    finished: boolean;
  }

  let todo: Todo[] = [
    {
      text: "Wake up 🛏️",
      finished: true,
    },
    {
      text: "Take some bath 🚿",
      finished: true,
    },
    {
      text: "Die 💀",
      finished: false,
    },
  ];

  function add() {
    todo = [
      ...todo,
      {
        text: "New goal",
        finished: false,
      },
    ];
  }

  function remove(index) {
    todo = todo.filter((t, i) => i !== index);
  }
</script>

<main>
  <h1>TODO 📔</h1>
  <ol>
    {#each todo as { finished, text }, index}
      <li>
        <span
          contenteditable
          bind:textContent={text}
          class={"title " + (finished && "finished")}
        />
        <input class="hoverable" type="checkbox" bind:checked={finished} />
        <span class="hoverable danger" on:click={() => remove(index)}>x</span>
      </li>
    {/each}
  </ol>
  <button on:click={add}>Add</button>
</main>

<style>
  main {
    text-align: center;
    padding: 1em;
    font-size: 1.5em;
    margin: 0 auto;
  }

  button {
    border: 1px solid black;
    border-bottom: 5px solid black;
    background: white;
    transition: all 0.07s;
  }

  button:hover {
    background: grey;
    cursor: pointer;
    color: white;
    transition: all 0.07s;
  }

  .title {
    padding: 5px 10px;
  }

  .danger {
    color: red;
  }

  .hoverable {
    cursor: pointer;
  }

  .finished {
    text-decoration-line: line-through;
    color: green;
    opacity: 0.5;
  }
</style>
