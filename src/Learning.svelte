<script lang="ts">
  import type { Action } from "svelte/action";
  import { words1 } from "./Words/Learning/lvl1.js";
  import { words2 } from "./Words/Learning/lvl2.js";
  import { words3 } from "./Words/Learning/lvl3.js";
  import { words4 } from "./Words/Learning/lvl4.js";
  import { words5 } from "./Words/Learning/lvl5.js";
  import { words6 } from "./Words/Learning/lvl6.js";
  import { words7 } from "./Words/Learning/lvl7.js";

  type NestedArray<T> = Array<Array<T>>;
  export function shuffleArray<T>(array: T[]): void {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1)); // выбираем индекс от 0 до текущего элемента включительно
      [array[i], array[j]] = [array[j], array[i]]; // меняем местами два элемента
    }
  }
  let words = words1;

  let isCorrectLetter = $state(true);
  let game = $state(true);
  let currentWord = $state("");

  let input = $state("");
  let level = $state(Number(localStorage.getItem("levelLearning")) ?? 1);

  let correctClicks = $state(
    Number(localStorage.getItem("correctClicksLearning")) ?? 0,
  );
  let incorrectClicks = $state(
    Number(localStorage.getItem("incorrectClicksLearning")) ?? 0,
  );

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
  <div class="space-y-3 text-3xl">
    <div>Уровень {level}</div>
    <div>Пройдено на {Math.round((100 * score) / words.length)}%</div>
    <div class="font-mono py-5 flex whitespace-pre-wrap text-amber-200">
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
