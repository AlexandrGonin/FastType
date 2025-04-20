<script lang="ts">
    import type { Action } from "svelte/action";
    import { words } from "./Words/words.js";

    let isCorrectLetter = $state(true);
    let game = $state(true);
    let currentWord = $state("");
    let input = $state("");
    let score = $state(Number(localStorage.getItem("score")) ?? 0);
    $effect(() => localStorage.setItem("score", score.toString()));
    let currentNum = $state(0);

    function startGame() {
        game = true;
        currentWord = words[currentNum];
        score = 0;
        input = "";
    }

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
    });

    const init: Action = (el) => {
        el.focus();
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
    {/if}
</div>
