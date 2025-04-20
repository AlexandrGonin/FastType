<script>
    import GameCommon from "./Game_common.svelte";
    import GameTimer from "./Game_timer.svelte";
    import Error404 from "./Error404.svelte";
    import Learning from "./Learning.svelte";

    const views1 = ["Selector", "Common", "Timer", "Learning"];
    let currentView = $state(views1[0]);
</script>

<main>
    {#if currentView == "Common"}
        <button
            class=" mx-10 my-5 px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform bg-black"
            onclick={() => (currentView = views1[0])}>⬅ Вернуться назад</button
        >
        <GameCommon />
    {:else if currentView == "Timer"}
        <button
            class=" mx-10 my-5 px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform bg-black"
            onclick={() => (currentView = views1[0])}>⬅ Вернуться назад</button
        >
        <GameTimer />
    {:else if currentView == "Learning"}
        <button
            class=" mx-10 my-5 px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform bg-black"
            onclick={() => (currentView = views1[0])}>⬅ Вернуться назад</button
        >
        <Learning />
    {:else if currentView == "Selector"}
        <div
            class="mx-40 my-10 px-10 py-5 w-60 rounded-lg items-center text-black bg-gradient-to-br from-gray-400 to-gray-200"
        >
            Выберите режим:
        </div>
        <div
            class="grow flex justify-center items-center gap-100 bg-gray-400 rounded-lg mx-40 p-10"
        >
            <button
                class="px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform font-bold text-3xl text-gray-500 border-1 border-gray-300 bg-gray-300 w-50 h-50"
                onclick={() => (currentView = views1[1])}>Обычный</button
            >
            <button
                class="px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform font-bold text-3xl text-gray-500 border-1 border-gray-300 bg-gray-300 w-50 h-50"
                onclick={() => (currentView = views1[2])}>На время</button
            >
            <button
                class="px-4 py-1 rounded-lg cursor-pointer active:scale-80 transition-transform font-bold text-3xl text-gray-500 border-1 border-gray-300 bg-gray-300 w-50 h-50"
                onclick={() => (currentView = views1[3])}>Обучение</button
            >
        </div>
    {/if}
</main>
