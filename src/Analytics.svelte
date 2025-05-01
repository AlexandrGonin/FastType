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

  let correctClicks = correctClicksCommon + correctClicksTime;
  let incorrectClicks = incorrectClicksCommon + incorrectClicksTime;
</script>

<div class="flex justify-center flex-col m-20 bg-violet-400 rounded-lg">
  <div class="h-50 m-10 rounded-lg bg-violet-300 p-5">
    <b> Общая статистика </b><br />
    Точность: {Math.round(
      100 * (correctClicks / (correctClicks + incorrectClicks)),
    )}% <br />
    Верных нажатий: {correctClicks} <br />
    Неверных нажатий: {incorrectClicks}
  </div>
  <div class="flex justify-center m-10 flex-row gap-x-10">
    <div class="bg-violet-300 w-full h-50 rounded-lg p-5">
      <b> Обычный режим </b><br />
      Точность: {Math.round(
        100 *
          (correctClicksCommon / (correctClicksCommon + incorrectClicksCommon)),
      )}% <br />
      Верных нажатий: {correctClicksCommon} <br />
      Неверных нажатий: {incorrectClicksCommon}
    </div>
    <div class="bg-violet-300 w-full h-50 rounded-lg p-5">
      <b> На время </b><br />
      Точность: {Math.round(
        100 * (correctClicksTime / (correctClicksTime + incorrectClicksTime)),
      )}% <br />
      Верных слов: {correctClicksTime} <br />
      Неверных слов: {incorrectClicksTime}
    </div>
    <div class="bg-violet-300 w-full h-50 rounded-lg p-5">Обучение</div>
  </div>
</div>
