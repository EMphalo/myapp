<script>
    import Nested from "./Nested.svelte";
    let textToDisplay = 'this is string containing <h1><i><strong>HTML!</strong></i></h1>';

    let count = 0;
    function increment() {
        count += 1;
    }

    $: doubled = count * 2;

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
<Nested />

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
