<script lang="ts">
  import type { Action } from "svelte/action";
  import { words1 } from "./Words/Learning/lvl1.js";
  import { words2 } from "./Words/Learning/lvl2.js";
  import { words3 } from "./Words/Learning/lvl3.js";
  import { words4 } from "./Words/Learning/lvl4.js";
  import { words5 } from "./Words/Learning/lvl5.js";
  import { words6 } from "./Words/Learning/lvl6.js";
  import { words7 } from "./Words/Learning/lvl7.js";
  import arms_pic from "./assets/arms_pic.jpg";

  let words = $state(words1);

  let isCorrectLetter = $state(true);
  let game = $state(true);
  let currentWord = $state("");
  let isViewOfPic = $state(false);

  let input = $state("");
  let level = $state(Number(localStorage.getItem("levelLearning")) ?? 1);
  let isLevelChange = $state(false);

  function changeCond() {
    isLevelChange = !isLevelChange;
  }

  function updateWords() {
    if (!level) {
      level = 1;
    }
    if (level == 1) {
      words = words1;
    }
    if (level == 2) {
      words = words2;
    }
    if (level == 3) {
      words = words3;
    }
    if (level == 4) {
      words = words4;
    }
    if (level == 5) {
      words = words5;
    }
    if (level == 6) {
      words = words6;
    }
    if (level == 7) {
      words = words7;
    }
    if (level == 8) {
      words = [""];
    }
  }

  function changeLevel1() {
    words = words1;
    changeCond();
    level = 1;
    score = 1;
    currentWord = words[score];
  }
  function changeLevel2() {
    words = words2;
    changeCond();
    level = 2;
    score = 1;
    currentWord = words[score];
  }
  function changeLevel3() {
    changeCond();
    words = words3;
    level = 3;
    score = 1;
    currentWord = words[score];
  }
  function changeLevel4() {
    changeCond();
    words = words4;
    level = 4;
    score = 1;
    currentWord = words[score];
  }
  function changeLevel5() {
    changeCond();
    words = words5;
    level = 5;
    score = 1;
    currentWord = words[score];
  }
  function changeLevel6() {
    changeCond();
    words = words6;
    level = 6;
    score = 1;
    currentWord = words[score];
  }
  function changeLevel7() {
    changeCond();
    words = words7;
    level = 7;
    score = 1;
    currentWord = words[score];
  }

  function changeCondPic() {
    isViewOfPic = !isViewOfPic;
  }

  updateWords();

  let correctClicks = $state(
    Number(localStorage.getItem("correctClicksLearning")) ?? 0,
  );
  let incorrectClicks = $state(
    Number(localStorage.getItem("incorrectClicksLearning")) ?? 0,
  );

  let score = $state(Number(localStorage.getItem("scoreLearning")) ?? 0);
  if (score) {
    score -= 1;
  }
  if (correctClicks) {
    correctClicks -= 1;
  }
  $effect(() => localStorage.setItem("levelLearning", level.toString()));
  $effect(() => localStorage.setItem("scoreLearning", score.toString()));

  $effect(() =>
    localStorage.setItem("correctClicksLearning", correctClicks.toString()),
  );
  $effect(() =>
    localStorage.setItem("incorrectClicksLearning", incorrectClicks.toString()),
  );

  $effect(() => {
    if (Math.round((100 * score) / words.length) >= 100) {
      level += 1;
      score = 0;
    }
  });

  $effect(() => {
    if (currentWord == input) {
      isCorrectLetter = true;
      currentWord = words[score];
      input = "";
      score += 1;
      correctClicks += 1;
    }
    if (!currentWord.startsWith(input)) {
      input = "";
      isCorrectLetter = false;
      incorrectClicks += 1;
    }
    if (words.length - score) {
    }
    if (input) {
      input = "";
    }
  });

  const init: Action = (el) => {
    if (el != null) {
      el.focus();
    }
  };
</script>

<svelte:window onclick={() => init(document.getElementById("input")!)} />

<div class="p-50 space-y-5">
  <div class="space-y-3 text-3xl flex flex-col gap-2">
    <div>
      <button
        class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
        onclick={changeCondPic}
      >
        Расположение рук
      </button>
    </div>
    <div>
      <button
        class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
        onclick={changeCond}>Сменить уровень</button
      >
    </div>
    <div>Уровень {level}</div>

    <div>Пройдено на {Math.round((100 * score) / words.length)}%</div>
    <div class="font-mono flex whitespace-pre-wrap text-amber-200">
      <div style="color: {isCorrectLetter ? 'amber-200' : 'red'}">
        {words.slice(score - 1, score).join("")}
      </div>
      <div>
        {words.slice(score, score - 1 + 68).join("")}
      </div>
    </div>
    <div class="flex">
      <input
        id="input"
        type="text"
        placeholder="..."
        bind:value={input}
        class="font-mono"
        class:text-red-500={!currentWord.startsWith(input)}
      />
    </div>
  </div>
</div>
{#if isLevelChange}
  <div
    class="fixed top-0 left-0 w-screen h-screen bg-black/75 z-50 flex items-center justify-center text-white font-bold gap-5"
  >
    <button
      class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
      onclick={changeLevel1}>Уровень 1</button
    >
    <button
      class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
      onclick={changeLevel2}>Уровень 2</button
    >

    <button
      class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
      onclick={changeLevel3}>Уровень 3</button
    >
    <button
      class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
      onclick={changeLevel4}>Уровень 4</button
    >
    <button
      class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
      onclick={changeLevel5}>Уровень 5</button
    >
    <button
      class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
      onclick={changeLevel6}>Уровень 6</button
    >
    <button
      class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
      onclick={changeLevel7}>Уровень 7</button
    >
  </div>
{/if}
{#if isViewOfPic}
  <div
    class="fixed top-0 left-0 w-screen h-screen bg-black/75 z-50 flex items-center justify-center text-white font-bold gap-5"
  >
    <div class="m-100 flex flex-col">
      <img src={arms_pic} class="rounded-2xl m-10" />

      <button
        class="rounded-lg cursor-pointer active:scale-80 transition-transform bg-violet-500 p-2"
        onclick={changeCondPic}>ОК</button
      >
    </div>
  </div>
{/if}
