<script>
  let correctClicksCommon = $state(
    Number(localStorage.getItem("correctClicksCommon")) ?? 0,
  );
  let incorrectClicksCommon = $state(
    Number(localStorage.getItem("incorrectClicksCommon")) ?? 0,
  );

  let correctClicksTime = $state(
    Number(localStorage.getItem("correctClicksTime")) ?? 0,
  );
  let incorrectClicksTime = $state(
    Number(localStorage.getItem("incorrectClicksTime")) ?? 0,
  );

  let correctClicksLearning = $state(
    Number(localStorage.getItem("correctClicksLearing")) ?? 0,
  );
  let incorrectClicksLearning = $state(
    Number(localStorage.getItem("incorrectClicksLearning")) ?? 0,
  );

  let accuracyCommon = Math.round(
    100 * (correctClicksCommon / (correctClicksCommon + incorrectClicksCommon)),
  );
  let accuracyTime = Math.round(
    100 * (correctClicksTime / (correctClicksTime + incorrectClicksTime)),
  );
  let accuracyLearning = Math.round(
    100 *
      (correctClicksLearning /
        (correctClicksLearning + incorrectClicksLearning)),
  );

  let correctClicks =
    correctClicksCommon + correctClicksTime + correctClicksLearning;
  let incorrectClicks =
    incorrectClicksCommon + incorrectClicksTime + incorrectClicksLearning;
</script>

<div class="flex justify-center flex-col m-20 bg-violet-400 rounded-lg">
  <div class="h-50 m-10 rounded-lg bg-violet-300 p-5">
    <b> Общая статистика </b><br />
    Точность: {#if !Number.isNaN(correctClicks / (correctClicks + incorrectClicks))}
      {Math.round(100 * (correctClicks / (correctClicks + incorrectClicks)))}
    {:else}0{/if}%
    <br />
    Верных нажатий: {correctClicks} <br />
    Неверных нажатий: {incorrectClicks}
  </div>
  <div class="flex justify-center m-10 flex-row gap-x-10">
    <div class="bg-violet-300 w-full h-50 rounded-lg p-5">
      <b> Обычный режим </b><br />
      Точность: {#if !Number.isNaN(accuracyCommon)}
        {Math.round(
          100 *
            (correctClicksCommon /
              (correctClicksCommon + incorrectClicksCommon)),
        )}
      {:else}0{/if}%
      <br />
      Верных нажатий: {correctClicksCommon} <br />
      Неверных нажатий: {incorrectClicksCommon}
    </div>
    <div class="bg-violet-300 w-full h-50 rounded-lg p-5">
      <b> На время </b><br />
      Точность: {#if !Number.isNaN(accuracyTime)}
        {Math.round(
          100 * (correctClicksTime / (correctClicksTime + incorrectClicksTime)),
        )}
      {:else}0{/if}%
      <br />
      Верных слов: {correctClicksTime} <br />
      Неверных слов: {incorrectClicksTime}
    </div>
    <div class="bg-violet-300 w-full h-50 rounded-lg p-5">
      <b> Обучение </b><br />
      Точность: {#if !Number.isNaN(accuracyLearning)}
        {Math.round(
          100 *
            (correctClicksLearning /
              (correctClicksLearning + incorrectClicksLearning)),
        )}
      {:else}0{/if}%
      <br />
      Верных слов: {correctClicksLearning} <br />
      Неверных слов: {incorrectClicksLearning}
    </div>
  </div>
</div>
