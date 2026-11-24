<script lang="ts">
    import type { Task} from "../types";
    type Props = {
        task: Task;
        onToggle: (id: number) => void;
        onDelete: (id: number) => void;  
    };

    let { task, onToggle, onDelete } : Props= $props();
</script>

<li class:completed={task.completed}>
    <input
        type="checkbox"
        checked={task.completed}
        onchange={() => onToggle(task.id)}
        aria-label={task.completed ? "Marcar como incompleta" : "Marcar como completa"}
    />

    <span>{task.title}</span>
    <button
        class="delete"
        onclick={() => onDelete(task.id)}
        aria-label="Eliminar {task.title}"
        title="Eliminar {task.title}"
    >
    x
    </button>
</li>
<style>
    li {
        display: flex;
        gap: 0.75rem;
        align-items: center;
        padding: 0.75rem 1rem;
        background-color: #fff;
        border-radius: 8px;
    }

    li.completed span {
        text-decoration: line-through;
        opacity: 0.6;
    }

    input[type="checkbox"] {
        margin-right: 0.5rem;
    }

    span {
        flex: 1;
        overflow-wrap: anywhere;
    }

    .delete {
        border: 0;
        background: transparent;
        color: #b00020;
        font-size: 1.25rem;
        line-height: 1;
        cursor: pointer;
        padding: 0.25rem 0.5rem;
        border-radius: 6px;
    }

    .delete:hover {
            background: #fde8e8;
    }

</style>
