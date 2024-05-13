<script>
    import Nested from "./Nested.svelte";
    let textToDisplay = 'this is string containing <h1><i><strong>HTML!</strong></i></h1>';

    let count = 0;
    function increment() {
        count += 1;
    }

    $: doubled = count * 2;
    $: if (count ==10 ){
        alert(`maxmum of 10 has been reached!`);
        count = 0;
    }
    
    let numbers = [1, 2, 3, 4, 5];

    function addNumber() {

        numbers .push(numbers.length + 1);
        numbers = [...numbers, numbers.length + 1]
    }

    $: sum  = numbers.reduce((total, currentNumber) => total + currentNumber, 0);


</script>
<h1>Welcome to Svelt</h1>
<p>
    Introduction page
    {@html textToDisplay}
</p>
<p>{count} doubled is {doubled}</p>
<button on:click={increment}>
    Clicked {count}
    {count === 1 ? 'time' : 'times'}
</button>
<button on:click={addNumber}>
    Add a Number 
</button> 

<p>{numbers.join(' + ')} = {sum}</p>
<Nested answer = {43} />

<style>
    h1 {
        border-bottom: 0.5px solid blue;
    }
    button{
        border: 1px solid black;
        border-radius: 2px 2px;
        background-color: gray;
        font-size: large;
        padding: 1em 2em;
        color: white;
    }
</style>
