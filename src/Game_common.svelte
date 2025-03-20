<script lang="ts">
    import type { Action } from "svelte/action";
    import { words } from "./words.js";

    let game = $state(true);
    let currentWord = $state("");
    let input = $state("");
    let score = $state(0);
    let currentNum = $state(0);

    function startGame() {
        game = true;
        currentWord = words[currentNum];
        score = 0;
        input = "";
    }

    $effect(() => {
        if (currentWord == input && game) {
            currentWord = words[currentNum];
            input = "";
            score += 1;
            currentNum += 1;
        }
        if (!currentWord.startsWith(input)) {
            input = "";
        }
    });

    const init: Action = (el) => {
        el.focus();
    };
</script>

<svelte:window onclick={() => init(document.getElementById("input")!)} />

<div class="p-50 space-y-5">
    {#if game}
        <div class="space-y-3 text-3xl">
            <div class="font-mono py-5">
                {words.slice(currentNum - 1, currentNum - 1 + 50).join("")}
            </div>
            <div class="flex">
                <div>{score}.</div>
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
