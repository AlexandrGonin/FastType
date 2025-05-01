<script lang="ts">
  import type { Action } from "svelte/action";
  import { words } from "./Words/words.js";

  let game = $state(false);
  let currentWord = $state();
  let currentLetter = $state();
  let input = $state("");
  let score = $state(0);
  let timer = $state(0);
  let timerChoosed = $state(15);
  const times = [15, 30, 60];
  let currentView = $state(times[0]);
  let correctClicks = $state(
    Number(localStorage.getItem("correctClicksTime")) ?? 0,
  );
  let incorrectClicks = $state(
    Number(localStorage.getItem("incorrectClicksTime")) ?? 0,
  );

  $effect(() =>
    localStorage.setItem("correctClicksTime", correctClicks.toString()),
  );
  $effect(() =>
    localStorage.setItem("incorrectClicksTime", incorrectClicks.toString()),
  );

  export function shuffleArray<T>(array: T[]): void {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1)); // выбираем индекс от 0 до текущего элемента включительно
      [array[i], array[j]] = [array[j], array[i]]; // меняем местами два элемента
    }
  }

  shuffleArray(words);

  function changeTime(time: number) {
    timer = time;
    startGame;
  }

  function startGame() {
    shuffleArray(words);
    game = true;
    currentWord = String(words[0].join(""));
    score = 0;
    input = "";
    function decreaseTimer() {
      if (timer > 0) {
        timer -= 1;
        if (currentWord != input && game) {
          incorrectClicks += 1;
        }

        setTimeout(decreaseTimer, 1000);
      } else {
        game = false;
      }
    }
    decreaseTimer();
  }

  $effect(() => {
    if (currentWord == input && game) {
      score += 1;
      correctClicks += 1;
      currentWord = String(words[score].join(""));
      input = "";
    }
  });

  const init: Action = (el) => {
    el.focus();
  };
</script>

<svelte:window onclick={() => init(document.getElementById("input")!)} />
<div>
  <div class="flex justify-center text-2xl">Выберите время:</div>
  <div class="flex justify-center text-2xl my-5 gap-x-10">
    {#each times as time}
      <button
        class="rounded-lg bg-violet-500 p-2 my-5 cursor-pointer active:scale-80 transition-transform"
        class:bg-violet-700={timer == time}
        onclick={() => changeTime(time)}
      >
        {time} сек
      </button>
    {/each}
  </div>
</div>
<div class="px-40 py-20 space-y-5">
  <div class="text-4xl">
    <div class="mb-10">Счет: {score}</div>
    {#if !game}
      <button
        onclick={startGame}
        class=" rounded-lg bg-violet-500 p-2 my-5 cursor-pointer active:scale-80 transition-transform"
        >Играть</button
      >
    {/if}
  </div>

  {#if game}
    <div class="space-y-3 text-3xl">
      <div>Осталось {timer} секунд</div>
      <div class="text-amber-200">{String(currentWord)}</div>
      <input
        id="input"
        type="text"
        placeholder="..."
        bind:value={input}
        class="font-mono"
        class:text-red-500={!String(currentWord).startsWith(input)}
      />
    </div>
  {/if}
</div>
