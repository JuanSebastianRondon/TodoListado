<script lang="ts">
    let clicks = $state(0);
</script>

<main>
<h1>TodoListado </h1>
    <button onclick={() => clicks++}>
        Clicks: {clicks}
    </button>
</main>