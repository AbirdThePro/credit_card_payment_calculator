<script lang="ts">
  let balance:number = 0;
  let apr:number = 1;
  let minPayment:number = 1;
  let payment:number = 0;
  let total:number = 0;
  
  const calculate = () => {
    total = 0;
    let remainingBalance:number = balance;
    while (remainingBalance > payment) {
      total += payment;
      remainingBalance -= payment;
      remainingBalance *= (1 + ((apr / 12) / 100));
    }
    total += remainingBalance;
  };
</script>

<main>
  <div class="rounded-lg text-white border-2 border-emerald-400 border-solid h-fit m-5 p-5">
    <h2 class="text-center font-bold text-2xl mb-5 bg-gradient-to-r from-emerald-400 to-green-400 text-transparent bg-clip-text">
      Credit Card Loan Calculator
    </h2>
    <div class="flex">
      <p class="pr-[6.4rem] font-bold">Balance:</p>
      <input bind:value={balance} class="bg-slate-700 w-32 rounded" type="number" min="0">
    </div>
    <br>
    <div class="flex">
      <p class="pr-32 font-bold">APR:</p>
      <input bind:value={apr} class="float-left accent-emerald-200 transparent w-32 appearance-none rounded bg-slate-700" type="range" min="1" max="15" step="0.1">
      <p class="pl-2 float-right">
        {(Math.round(apr * 100) / 100).toFixed(1)}%
      </p>
    </div>
    <br>
    <div class="flex">
      <p class="pr-4 font-bold">Minimum Payment:</p>
      <input bind:value={minPayment} class="float-left transparent w-32 appearance-none rounded bg-slate-700" type="range" min="1" max="5" step="0.1">
      <p class="pl-2 float-right">
        {(Math.round(minPayment * 100) / 100).toFixed(1)}%
      </p>
    </div>
    <br>
    <div class="flex">
      <p class="pr-6 font-bold">Monthly Payment:</p>
      <input bind:value={payment} class="bg-slate-700 w-32 rounded" type="number" min={minPayment} max={balance}>
    </div>
    <div class="grid place-items-center mt-5">
      <button on:click={calculate} class="rounded p-2 bg-gradient-to-r from-emerald-500 to-green-400 active:bg-emerald-400">
        Calculate!
      </button>
    </div>
    <h2 class="pt-3 text-center text-2xl font-bold">
      Total: ${(Math.round(total * 100) / 100).toFixed(2)}
    </h2>
  </div>
</main>
