<script lang="ts">
    const words = [
      "print('hello')",
      "def hello():",
      "while count > 0:",
      "for i in range(5):",
      "return number",
      "from tkinter import *",
      "int(input())",
    ];
  
    let game = $state(false);
    let currentWord = $state("");
    let input = $state("");
    let score = $state(0);
    let timer = $state(0);
  
    function startGame() {
      game = true;
      currentWord = words[Math.floor(Math.random() * words.length)];
      score = 0;
      input = "";
      function decreaseTimer() {
        if (timer > 0) {
          timer -= 1;
          setTimeout(decreaseTimer, 1000);
        } else {
          game = false;
        }
      }
      timer = 15;
      decreaseTimer();
    }
  
    $effect(() => {
      if (currentWord == input && game) {
        currentWord = words[Math.floor(Math.random() * words.length)];
        input = "";
        score += 1;
      }
    });
  </script>
  
  <div class="p-5 space-y-5">
    <div>
      <div>Счет: {score}</div>
      <button onclick={startGame} class="text-blue-500">Играть</button>
    </div>
  
    {#if game}
      <div class="space-y-3 text-3xl">
        <div>{timer + 1} сек осталось</div>
        <div class="font-mono">{currentWord}</div>
        <input
          type="text"
          placeholder="..."
          bind:value={input}
          class="font-mono"
          class:text-red-500={!currentWord.startsWith(input)}
        />
      </div>
    {/if}
  </div>