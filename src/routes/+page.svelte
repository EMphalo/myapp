<script>
    import Nested from "./Nested.svelte";
    import PackageInfo from "./PackageInfo.svelte";
	// import { time } from "./stores";
    import { tweened } from "svelte/motion";
    import { cubicOut } from "svelte/easing";

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

        numbers.push(numbers.length + 1);
        numbers = [...numbers, numbers.length + 1]
    }

    $: sum  = numbers.reduce((total, currentNumber) => total + currentNumber, 0);

    const pkg = {
        name: 'svelte',
        speed: 'blazing',
        version: 4,
        website: 'http://svelte.dev'
    }

    const colors = ['red', 'green', 'blue', 'cyan', 'black','violet'];
    let selectedColor = colors[0];

    //time
    const formatter = new Intl.DateTimeFormat('en',
        {
            hour12:true,
            hour:'numeric',
            minute:'2-digit',
            second:'2-digit'
        }
    );

    const progress = tweened(0, {
        duration: 1000,
        easing: cubicOut
    });

    let selection = '';
    
    const handleSelectionChange = (e) => selection = document.getSelection();
    
</script>
<!--  -->

<progress value="{$progress}"/>

<svelte:document on:selectionchange={handleSelectionChange} />

<p>Selected Text: {selection} </p>

<button on:click={() => progress.set(0)}>
    0%
</button>
<button on:click={() => progress.set(0.25)}>
    25%
</button>
<button on:click={() => progress.set(0.5)}>
    50%
</button>
<button on:click={() => progress.set(0.75)}>
    75%
</button>
<button on:click={() => progress.set(1)}>
    100%
</button>
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

<PackageInfo {...pkg}/>

<h1 style="color: {selectedColor}"> 
    Pick a Colour    
</h1>

<div id="btn-group">
    {#each colors as color, i}
        <button
            aria-current={selectedColor ===color}
            aria-label = {color}
            style = "background:{color}"
            on:click={() => selectedColor = color}
            >{i +1}
        </button>
    {/each }
</div>

<style>
    progress {
        display: block;
        width: 100%;
    }
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
    h1 {
		transition: color 0.2s;
	}

	div {
		display: grid;
		grid-template-columns: repeat(7, 1fr);
		grid-gap: 5px;
		max-width: 400px;
	}

	#btn-group button {
		aspect-ratio: 1;
		border-radius: 50%;
		background: var(--color, #fff);
		transform: translate(-2px,-2px);
		filter: drop-shadow(2px 2px 3px rgba(0,0,0,0.2));
		transition: all 0.1s;
	}

	#btn-group button[aria-current="true"] {
		transform: none;
		filter: none;
		box-shadow: inset 3px 3px 4px rgba(255, 0, 0, 0.2);
	}
    .timeDisplay{
        color: #fff;
        box-shadow: inset 3px 3px 4px rgba(255, 0, 0, 0.2);
        background: linear-gradient(rgb(14, 169, 190),rgb(1, 11, 105),rgba(6, 141, 85, 0.918))
    }
</style>
