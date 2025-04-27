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
        <div>
            <div class="flex justify-center m-20 text-2xl">Выберите режим:</div>
            <div
                class="flex items-start justify-center w-full flex-wrap gap-40 p-4 md:p-8"
            >
                <button
                    class="px-4 py-1 rounded-3xl cursor-pointer active:scale-80 transition-transform font-thin text-2xl bg-violet-500 w-50 h-50"
                    onclick={() => (currentView = views1[1])}>Обычный</button
                >
                <button
                    class="px-4 py-1 rounded-3xl cursor-pointer active:scale-80 transition-transform font-thin text-2xl bg-violet-500 w-50 h-50"
                    onclick={() => (currentView = views1[2])}>На время</button
                >
                <button
                    class="px-4 py-1 rounded-3xl cursor-pointer active:scale-80 transition-transform font-thin text-2xl bg-violet-500 w-50 h-50"
                    onclick={() => (currentView = views1[3])}>Обучение</button
                >
            </div>
        </div>
    {/if}
</main>
