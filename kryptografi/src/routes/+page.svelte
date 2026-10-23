<script>
    let Tekst=$state("");
    let nokkel=$state(0);
    let resultat=$state("");
    let feilmelding=$state(""); 

    let text = $state("");
    let key2 = $state("");
    let result = $state("");
    let error = $state("");

    const ABC = "ABCDEFGHIJKLMNOPQRSTUVWXYZ";

    function kjorCaesar(retning){
        feilmelding="";
        resultat="";

        if (!Tekst.trim()) {
            feilmelding = "Tekstfeltet er tomt";
            return;
        }

        if (nokkel === null || nokkel<0||nokkel>25){
            feilmelding = "Nøkkelord må være mellom 0 og 25";
            return;
        }

        let midlertidigResultat="";

        for (let i = 0; i <Tekst.length; i++){
            const b = Tekst[i];

            if(b===" "){
                midlertidigResultat+=" ";
                continue;
            }

            const u = b.toUpperCase();
            const pos = ABC.indexOf(u);

            if (pos === -1){

                feilmelding="kun engelske bokstaver";
                return;

            }


            let nyPos=(pos+nokkel*retning)%26;
             if(nyPos<0)nyPos+=26;

            midlertidigResultat +=b===u
                ?ABC[nyPos]
                :ABC[nyPos].toLowerCase();
        }

    

    resultat=midlertidigResultat;

}



    function vigenere(dir) {
        error = "";
        result = "";

        if (!text.trim()) {
            error = "Tekstfeltet er tomt";
            return;
        }

        if (!key2.trim()) {
            error = "Nøkkelord er tomt";
            return;
        }

        if (!/^[A-Za-z]+$/.test(key2)) {
            error = "Nøkkelord må være engelske bokstaver";
            return;
        }

        let out = "";
        let upperKey = key2.toUpperCase();
        let keyIndex = 0;

        for (let char of text) {
            if (char === " ") {
                out += " ";
                continue;
            }

            let upperChar = char.toUpperCase();
            let pos = ABC.indexOf(upperChar);

            if (pos === -1) {
                error = "Teksten kan kun inneholde engelske bokstaver";
                return;
            }

            let shift = ABC.indexOf(upperKey[keyIndex % upperKey.length]);
            let newPos = (pos + shift * dir + 26) % 26;

            out += char === upperChar
                ? ABC[newPos]
                : ABC[newPos].toLowerCase();

            keyIndex++;
        }

        result = out;
    }
</script>
<h2>Caesar Cipher</h2>

<label>Tekst:
    <input type="text" bind:value={Tekst}>
</label>

<label>Nøkkeltall:
    <input type="number" bind:value={nokkel}>
</label>

<button onclick={() => kjorCaesar(1)}>Krypter</button>
<button onclick={() => kjorCaesar(-1)}>Dekrypter</button>

{#if feilmelding}<p>{feilmelding}</p>{/if}
{#if resultat}<p>Resultat: <strong>{resultat}</strong></p>{/if}



<h2>Vigenère</h2>

<label>Tekst:
    <input bind:value={text}>
</label>

<label>Nøkkelord:
    <input bind:value={key2}>
</label>

<button onclick={() => vigenere(1)}>Krypter</button>
<button onclick={() => vigenere(-1)}>Dekrypter</button>

{#if error}<p>{error}</p>{/if}
{#if result}<p>Resultat: <strong>{result}</strong></p>{/if}
