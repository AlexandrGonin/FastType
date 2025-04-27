<script lang="ts">
    import type { Action } from "svelte/action";
    import { words } from "./Words/words.js";

    type NestedArray<T> = Array<Array<T>>;
    function shuffleArray<T>(array: T[]): void {
        for (let i = array.length - 1; i > 0; i--) {
            const j = Math.floor(Math.random() * (i + 1)); // выбираем индекс от 0 до текущего элемента включительно
            [array[i], array[j]] = [array[j], array[i]]; // меняем местами два элемента
        }
    }
    const flattenNestedList = <T,>(nestedList: NestedArray<T>): T[] => {
        return nestedList.reduce(
            (acc: T[], currentValue: T[]) => acc.concat(currentValue),
            [] as T[],
        );
    };
    shuffleArray(words);
    let words1 = flattenNestedList(words);
    let isCorrectLetter = $state(true);
    let game = $state(true);
    let currentWord = $state("");
    let input = $state("");
    let score = $state(Number(localStorage.getItem("score")) ?? 0);
    $effect(() => localStorage.setItem("score", score.toString()));
    let currentNum = $state(0);

    function startGame() {
        game = true;
        currentWord = words1[currentNum];
        score = 0;
        input = "";
    }

    $effect(() => {
        if (currentWord == input) {
            isCorrectLetter = true;
            currentWord = words1[currentNum];
            input = "";
            score += 1;
            currentNum += 1;
        }
        if (!currentWord.startsWith(input)) {
            input = "";
            isCorrectLetter = false;
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
    {#if currentNum}
        <div class="space-y-3 text-3xl">
            <div>
                Прогресс: {Number(localStorage.getItem("score"))} символов
            </div>
            <div class="font-mono py-5 flex whitespace-pre-wrap">
                <div style="color: {isCorrectLetter ? 'white' : 'red'}">
                    {words1.slice(currentNum - 1, currentNum).join("")}
                </div>
                <div>
                    {words1.slice(currentNum, currentNum - 1 + 68).join("")}
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
    {/if}
</div>
