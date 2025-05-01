<script lang="ts">
  import type { Action } from "svelte/action";
  import { wordsExp } from "./Words/Learning/lvl1.js";
  let wordsShuf = $state(wordsExp);
  let words: string[] = $state(wordsShuf);

  type NestedArray<T> = Array<Array<T>>;
  export function shuffleArray<T>(array: T[]): void {
    for (let i = array.length - 1; i > 0; i--) {
      const j = Math.floor(Math.random() * (i + 1)); // выбираем индекс от 0 до текущего элемента включительно
      [array[i], array[j]] = [array[j], array[i]]; // меняем местами два элемента
    }
  }
  export const flattenNestedList = <T,>(nestedList: NestedArray<T>): T[] => {
    return nestedList.reduce(
      (acc: T[], currentValue: T[]) => acc.concat(currentValue),
      [] as T[],
    );
  };
  for (let x = 0; x < 5; x += 1) {
    shuffleArray(wordsShuf);
    words.push(
      wordsShuf[0],
      wordsShuf[1],
      wordsShuf[2],
      wordsShuf[3],
      wordsShuf[4],
      wordsShuf[5],
    );
  }
  // let words1 = flattenNestedList(words);
  let isCorrectLetter = $state(true);
  let game = $state(true);
  let currentWord = $state("");
  let input = $state("");
  let score = $state(Number(localStorage.getItem("scoreLearning")) ?? 0);
  if (score) {
    score -= 1;
  }
  $effect(() => localStorage.setItem("scoreLearning", score.toString()));
  let currentNum = $state(0);

  $effect(() => {
    if (currentWord == input) {
      isCorrectLetter = true;
      currentWord = words[currentNum];
      input = "";
      score += 1;
      currentNum += 1;
    }
    if (!currentWord.startsWith(input)) {
      input = "";
      isCorrectLetter = false;
    }
    if (words.length - currentNum) {
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
    <div class="font-mono py-5 flex whitespace-pre-wrap">
      <div style="color: {isCorrectLetter ? 'white' : 'red'}">
        {words.slice(currentNum - 1, currentNum).join("")}
      </div>
      <div>
        {words.slice(currentNum, currentNum - 1 + 68).join("")}
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
