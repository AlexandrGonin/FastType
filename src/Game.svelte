<script>
    import GameCommon from "./Game_common.svelte";
    import GameTimer from "./Game_timer.svelte";
    import Error404 from "./Error404.svelte";

    const views1 = ["Common", "Timer"];
    let currentView = $state(views1[0]);
</script>

<main>
    {#if currentView == "Statistics"}
        <div>statistics</div>
    {:else if currentView == "Common"}
        <GameCommon />
    {:else if currentView == "Timer"}
        <GameTimer />
    {:else}
        <Error404 />
    {/if}
</main>
