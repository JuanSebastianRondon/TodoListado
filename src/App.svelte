<script lang="ts">
  import type { Task } from "./lib/types";
  import { tick } from "svelte";  
  import TaskItem from "./lib/components/TaskItem.svelte";
       
  function toggleTask(id: number){
    const task = tasks.find((t) => t.id === id);
      if (task) {
        task.completed = !task.completed;
      }
  }

  function deleteTask(id: number){
    tasks = tasks.filter((t) => t.id !== id);
  }

    let tasks = $state<Task[]>([
        { id: 1, title: "Diseñar la interfaz", completed: false },
        { id: 2, title: "Conectar SQLite", completed: true },
    ]);
    let draft = $state("");
    let inputEl= $state<HTMLInputElement | null>(null);
    let nextId = 3;

        async function addTask(event: SubmitEvent) {
            
            event.preventDefault();
            const title= draft.trim();

            if (!title) return;
            tasks.push({id: nextId++, title, completed: false});
            draft= "";

            await tick(); //Espera a que el DOM se actualice antes de enfocar el input
            inputEl?.focus(); // devuelve el foco para escribir el siguiente
        
        }

        

</script>

<main class="app">
  <h1>TodoListado</h1>

    <form class="task-form" onsubmit={addTask}>
        <label class="sr-only" for= "new-task">
            Nueva tarea:
        </label>
        <input
        id="new-task"
        bind:this={inputEl}
        bind:value={draft}
        placeholder="¿Que hay que hacer?"
        autoComplete="off"
        maxlength="100"
        />
        <button type="submit" disabled={!draft.trim()}>
            Agregar
        </button>
    </form>


  <ul class="task-list">
    {#each tasks as task (task.id)}
    <TaskItem {task} 
      onToggle={toggleTask}
      onDelete={deleteTask} />
    {/each}
  </ul>
</main>