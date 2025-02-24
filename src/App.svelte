<script>
  import Game from "./Game.svelte";
  import Menu from "./Menu.svelte";
  import Error404 from "./Error404.svelte";

  const views = ["Home", "Statistics", "Friends", "test"];
  let currentView = $state(views[0]);
</script>

<main
  class="h-dvh flex flex-col bg-gradient-to-br from-blue-700 via-violet-600 to-pink-400"
>
  <header>
    <nav>
      <ul class="bg-gray-800">
        <div class="p-5 gap-1 flex items-center justify-center">
          {#each views as view}
            <button
              class="px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform"
              class:bg-black={currentView == view}
              onclick={() => (currentView = view)}
            >
              {view}
            </button>
          {/each}
        </div>
      </ul>
    </nav>
  </header>

  <!-- проверка на текущую страницу -->
  {#if currentView == "Statistics"}
    <div>statistics</div>
  {:else if currentView == "Friends"}
    <div>friends</div>
  {:else if currentView == "Home"}
    <Menu />
  {:else}
    <Error404 />
  {/if}
</main>
