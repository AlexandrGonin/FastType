<script>
  import Game from "./Game.svelte";
  import Menu from "./Menu.svelte";
  import Error404 from "./Error404.svelte";
  import logo from "./assets/logo.svg";

  const views = ["Главная", "Играть"];
  let currentView = $state(views[0]);
</script>

<main
  class="h-dvh flex flex-col bg-gradient-to-br from-blue-1000 via-blue-800 to-blue-500"
>
  <header class="p-5 flex gap-3 items-center bg-gray-800">
    <button
      class="px-4 py-1 rounded-lg cursor-pointer active:scale-95 transition-transform"
    >
      <img src={logo} alt="LOGO" class="size-16" />
    </button>
    <nav class="grow flex justify-center items-center gap-1">
      {#each views as view}
        <button
          class="px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform"
          class:bg-black={currentView == view}
          onclick={() => (currentView = view)}
        >
          {view}
        </button>
      {/each}
    </nav>
    <div class="size-16"></div>
  </header>

  <!-- проверка на текущую страницу -->
  {#if currentView == "Главная"}
    <Menu />
  {:else if currentView == "Играть"}
    <Game />
  {:else}
    <Error404 />
  {/if}
</main>
