<script lang="ts">
    import type { Action } from "svelte/action";
    const words = [
        "print('hello')",
        "def hello():",
        "while count > 0:",
        "for i in range(5):",
        "return number",
        "from tkinter import *",
        "int(input())",
    ];

    let game = $state(true);
    let currentWord = $state("");
    let input = $state("");
    let score = $state(1);

    function startGame() {
        game = true;
        currentWord = words[Math.floor(Math.random() * words.length)];
        score = 0;
        input = "";
    }

    $effect(() => {
        if (currentWord == input && game) {
            currentWord = words[Math.floor(Math.random() * words.length)];
            input = "";
            score += 1;
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
            <div class="font-mono py-5">{currentWord}</div>
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
