<script lang="ts">
  const numbers=["1", "2", "3", "4", "5", "6","7","8","9","0","."]
  const operations=["/","x","-","+","="]

  let selectedOperation = "";
  let display = "";
  let firstNumber = "";
  let secondNumber = "";
  let isDisplayingResults = false;

  const handleOperationClick = (operation: string) => {
    if (!firstNumber) return;
    if (operation === "=") {
      if (!secondNumber) return;
      const firstNum = parseInt(firstNumber);
      const secondNum = parseInt(secondNumber);

      let results = "";

      switch (selectedOperation) {
        case "/":
          results = (firstNum / secondNum).toFixed(2);
          break;
        case "x":
          results = (firstNum * secondNum).toFixed(2);
          break;
        case "+":
          results = (firstNum + secondNum).toFixed(2);
          break;
        case "-":
          results = (firstNum - secondNum).toFixed(2);
          break;
      }

      display = results;
      isDisplayingResults = true;
    }
    selectedOperation = operation;
  };

  const handleClear = () => {
    firstNumber = "";
    secondNumber = "";
    selectedOperation = "";
    display = "";
    isDisplayingResults = false;
  };

  const handleNumberClick = (number: string) => {
    if (isDisplayingResults) {
      handleClear();
    }
    if (display === "" && number === "0") return;
    if (number === "." && display.includes(".")) return;

    if (!selectedOperation) {
      if (display === "" && number === ".") {
        firstNumber = "0.";
        return (display = firstNumber);
      }
      firstNumber = `${firstNumber}${number}`;
      return (display = firstNumber);
    } else {
      if (display === "" && number === ".") {
        secondNumber = "0.";
        return (display = secondNumber);
      }
      secondNumber = `${secondNumber}${number}`;
      return (display = secondNumber);
    }
  };
</script>



<main class="w-[100vw] h-[100vh] flex items-center justify-center">

    <div class="bg-slate-950  w-[260px] p-5 border rounded-2xl">
        <div class="flex flex-col gap-5">
            <div class="bg-neutral-500 bg-opacity-45 rounded-md w-full h-12 text-white text-2xl text-right p-2">{display}</div>
            <div class="flex gap-2">
                <div class="flex flex-wrap gap-2 text-2xl font-[400]">
                    <button on:click={handleClear} class="w-full h-12 rounded-full bg-neutral-500 text-white ">C</button>
                    {#each numbers as number(number)}
                    <button on:click={() => handleNumberClick(number)}
                    class="h-12  bg-neutral-500 rounded-full text-white {number === '0' ? 'w-[104px]' : 'w-12'} hover:shadow-lg ">{number}</button>
                    {/each}
                </div>
    
                <div class="flex flex-col gap-2 text-2xl font-[400] text-white ">
                    {#each operations as operation(operation) }
                    <button on:click = {() => handleOperationClick(operation)} class= "h-12 w-12 {operation === selectedOperation? 'bg-slate-400' : ' bg-amber-500'} rounded-full text-white">{operation}</button>
                    {/each}
                </div>
    
            </div>
        </div>
    </div>

</main>




