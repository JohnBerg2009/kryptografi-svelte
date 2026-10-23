<script>
    let text=$state("");
    let key= $state("");
    let result=$state("");
    let error=$state("");

    const ABC = "ABCDEFGHIJKLMNOPQRSTUVWXYZ"

    function vigenere(dir){
        error="";
        result="";
        
        if (!text.trim()){
            error="tekstfeltet er tomt";
            return;
        }

        if (!key.trim()){
            error="nøkkelord er tomt";
            return;
        }

        if (!/^[A-Za-z]+$/.test(key)) { //KI
            error = "nøkkelord må være engelske bokstaver";
            return;
        }

        let out ="";

        let upperKey = key.toUpperCase(),
        let keyindex=0;

        for(let char of)

    }
    

</script>

<h2>vigenere</h2>

<label>text:
    <input bind:value={text}>
</label>

<label>nøkkelord:
    <input bind:value={key}>
</label>

<button onclick={() => vigenere(1)}>kryptere</button>
<button onclick={() => vigenere(-1)}>dekryptere</button>

{#if error} <p>{error}</p>{/if}
{#if result} <p>Resultat: <strong>{result}</strong></p>{/if}