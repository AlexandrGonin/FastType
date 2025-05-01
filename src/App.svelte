<script>
  import Game from "./Game.svelte";
  import Menu from "./Menu.svelte";
  import Error404 from "./Error404.svelte";
  import logo from "./assets/logo.svg";
  import Analytics from "./Analytics.svelte";

  const views = ["Главная", "Играть", "Аналитика"];
  let currentView = $state(views[0]);
</script>

<main class="h-dvh flex flex-col bg-gradient-to-t from-purple-700 to-blue-700">
  <div class="min-h-full lg:hidden">
    <div class="p-5">
      Это приложение предназначено для пачати на клавиатуре, используйте ПК
    </div>
  </div>
  <div class="hidden sm:block">
    <header class="p-5 flex gap-3 items-center bg-gray-800">
      <button
        class="px-4 py-1 rounded-lg cursor-pointer active:scale-95 transition-transform"
        onclick={() => (currentView = views[0])}
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
      <button
        onclick={() => (currentView = views[1])}
        class="my-25 text-2xl px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 w-75 ml-40"
      >
        Начать тренировку
      </button>
    {:else if currentView == "Играть"}
      <Game />
    {:else if currentView == "Аналитика"}
      <Analytics />
    {:else}
      <Error404 />
    {/if}
  </div>
</main>
