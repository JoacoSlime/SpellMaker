<script>
    import { createEventDispatcher } from 'svelte';
    import {fs} from "@tauri-apps/api";
    import {BaseDirectory} from "@tauri-apps/api/fs";

    const dispatch = createEventDispatcher()

    export let data = {
        tecnica : {
            creo: 0,
            muto: 0,
            intellego: 0,
            rego: 0,
            perdo: 0
        },
        forma : {
            corpus: 0,
            herbam: 0,
            animal: 0,
            ignem: 0,
            terram: 0,
            auram: 0,
            imaginem: 0,
            mentem: 0,
            vim: 0
        },
        inteligencia : 0,
        teoriaMagica : 0
    };

    let fieldInteligencia = data.inteligencia;
    let fieldTeoriaMagica = data.teoriaMagica;
    let fieldCreo = data.tecnica.creo;
    let fieldMuto = data.tecnica.muto;
    let fieldIntellego = data.tecnica.intellego;
    let fieldRego = data.tecnica.rego;
    let fieldPerdo = data.tecnica.perdo;
    let fieldCorpus = data.forma.corpus;
    let fieldHerbam = data.forma.herbam;
    let fieldAnimal = data.forma.animal;
    let fieldIgnem = data.forma.ignem;
    let fieldTerram = data.forma.terram;
    let fieldAuram = data.forma.auram;
    let fieldAquam = data.forma.aquam;
    let fieldImaginem = data.forma.imaginem;
    let fieldMentem = data.forma.mentem;
    let fieldVim = data.forma.vim;

    // Reverse values: data.name.name= fieldName


    function formToData(){
        data.inteligencia = fieldInteligencia;
        data.teoriaMagica = fieldTeoriaMagica;
        data.tecnica.creo = fieldCreo;
        data.tecnica.muto = fieldMuto;
        data.tecnica.intellego = fieldIntellego;
        data.tecnica.rego = fieldRego;
        data.tecnica.perdo = fieldPerdo;
        data.forma.corpus = fieldCorpus;
        data.forma.herbam = fieldHerbam;
        data.forma.animal = fieldAnimal;
        data.forma.ignem = fieldIgnem;
        data.forma.terram = fieldTerram;
        data.forma.auram = fieldAuram;
        data.forma.aquam = fieldAquam;
        data.forma.imaginem = fieldImaginem;
        data.forma.mentem = fieldMentem;
        data.forma.vim = fieldVim;

        fs.writeTextFile({
            contents: JSON.stringify(data),
            path: "data.json"
        }, {dir: BaseDirectory.AppData}).catch((err) => {
            console.log(err)
        })
        dispatch('next')
    }
</script>

<main class="first_start">
    <h3>Configuración</h3>
    <hr>
    <div>
        <h4>Ingresa los datos:</h4>
        <form on:submit|preventDefault={formToData}>
            <div>
                <h5>Características:</h5>
                <div>
                    <label for="fieldInteligencia">Inteligencia: </label>
                    <input type="number" id="fieldInteligencia" name="fieldInteligencia" required bind:value={fieldInteligencia}>
                </div>
                <div>
                    <label for="fieldTeoriaMagica">Teoria Mágica: </label>
                    <input type="number" id="fieldTeoriaMagica" name="fieldTeoriaMagica" required bind:value={fieldTeoriaMagica}>
                </div>
            </div>
            <br>
            <div>
                <h5>Tecnicas</h5>
                <div>
                    <label for="fieldCreo">Creo: </label>
                    <input type="number" id="fieldCreo" name="fieldCreo" required  bind:value={fieldCreo}>
                </div>
                <div>
                    <label for="fieldMuto">Muto: </label>
                    <input type="number" id="fieldMuto" name="fieldMuto" required  bind:value={fieldMuto}>
                </div>
                <div>
                    <label for="fieldIntellego">Intellego: </label>
                    <input type="number" id="fieldIntellego" name="fieldIntellego" required  bind:value={fieldIntellego}>
                </div>
                <div>
                    <label for="fieldRego">Rego: </label>
                    <input type="number" id="fieldRego" name="fieldRego" required  bind:value={fieldRego}>
                </div>
                <div>
                    <label for="fieldPerdo">Perdo: </label>
                    <input type="number" id="fieldPerdo" name="fieldPerdo" required  bind:value={fieldPerdo}>
                </div>
            </div>
            <br>
            <div>
                <h5>Formas</h5>
                <div>
                    <label for="fieldCorpus">Corpus: </label>
                    <input type="number" id="fieldCorpus" name="fieldCorpus" required  bind:value={fieldCorpus}>
                </div>
                <div>
                    <label for="fieldHerbam">Herbam: </label>
                    <input type="number" id="fieldHerbam" name="fieldHerbam" required  bind:value={fieldHerbam}>
                </div>
                <div>
                    <label for="fieldAnimal">Animal: </label>
                    <input type="number" id="fieldAnimal" name="fieldAnimal" required  bind:value={fieldAnimal}>
                </div>
                <div>
                    <label for="fieldIgnem">Ignem: </label>
                    <input type="number" id="fieldIgnem" name="fieldIgnem" required  bind:value={fieldIgnem}>
                </div>
                <div>
                    <label for="fieldTerram">Terram: </label>
                    <input type="number" id="fieldTerram" name="fieldTerram" required  bind:value={fieldTerram}>
                </div>
                <div>
                    <label for="fieldAuram">Auram: </label>
                    <input type="number" id="fieldAuram" name="fieldAuram" required  bind:value={fieldAuram}>
                </div>
                <div>
                    <label for="fieldAquam">Aquam: </label>
                    <input type="number" id="fieldAquam" name="fieldAquam" required  bind:value={fieldAquam}>
                </div>
                <div>
                    <label for="fieldImaginem">Imaginem: </label>
                    <input type="number" id="fieldImaginem" name="fieldImaginem" required  bind:value={fieldImaginem}>
                </div>
                <div>
                    <label for="fieldMentem">Mentem: </label>
                    <input type="number" id="fieldMentem" name="fieldMentem" required  bind:value={fieldMentem}>
                </div>
                <div>
                    <label for="fieldVim">Vim: </label>
                    <input type="number" id="fieldVim" name="fieldVim" required  bind:value={fieldVim}>
                </div>
            </div>
            <br>
            <button type="submit" id="upload">Cargar</button>
        </form>
    </div>

</main>

<style>
    hr {
        width: 50%;
    }
    *{
        margin-left: auto;
        margin-right: auto;
    }
    form{
        display: flex;
        flex-direction: column;
        flex-flow: column;
        justify-content: center;
    }
    label{
        text-align: left;
        display: inline-block;
        width: 150px;
    }
    input{
        max-width: 45px;
        max-height: 30px;
        text-align: center;
    }
</style>