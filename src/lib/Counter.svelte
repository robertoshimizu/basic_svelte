<script lang="ts">

  // Reactivity Assignments
  let count: number = 0

  const increment = () => {
    count += 1
    addNumbertoVector()
  }

  let numbers = [];

  function addNumbertoVector() {
    // Spread Syntax
    
    // Assign numbers
    // to itself to tell the compiler it has changed
		numbers = [...numbers, numbers.length + 1];
	}

// Reactivity Declarations
  $: sum = numbers.reduce((t, n) => t + n, 0);
 
  $: doubled = count * 2;

  // run arbitrary statements reactively
  $: if (count >= 10) {
	alert('count is dangerously high!')
	count = 9;
}
</script>

<button class="card" on:click={increment}>
  count is {count}
</button>

<p>{count} doubled is {doubled}</p>

<p>Numbers are: {numbers}</p>

<p>Sum of array is: {sum}</p>


