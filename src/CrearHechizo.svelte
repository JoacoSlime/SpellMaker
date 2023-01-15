<script>
    export let data;
    export let totalLaboratorio;

    let fieldSimilar = 0;
    let fieldInestable = 0;
    let fieldComponentes = 0;
    let fieldNivelBase = 0;
    let fieldAlcance = 0;
    let fieldDuracion = 0;
    let checkObjetivo = false;
    let checkSentido = false;
    let fieldObjetivo = 0;
    let fieldTamano = 0;
    let fieldSentido = 0;
    let totalHechizo;
    let nivelHechizo = 0;

    function calcularTotalHechizo(){
        // Make totalHechizo equal to the sum of totalLaboratorio and add a 1 for each checked box
        totalHechizo = totalLaboratorio + fieldSimilar;
        totalHechizo += fieldInestable * 3;
        totalHechizo += fieldComponentes;
        nivelHechizo = fieldNivelBase;
        nivelHechizo += fieldAlcance;
        nivelHechizo += fieldDuracion;
        nivelHechizo += checkObjetivo * (fieldObjetivo + fieldTamano);
        nivelHechizo += checkSentido * fieldSentido;
        if (nivelHechizo > 5){
            nivelHechizo = 5 + (nivelHechizo - 5) * 5;
        }
    }

    calcularTotalHechizo();

    $: fieldSimilar, fieldInestable, fieldComponentes, fieldNivelBase, fieldAlcance, fieldDuracion, checkObjetivo, fieldObjetivo, fieldTamano, checkSentido, fieldSentido, calcularTotalHechizo();
</script>

<body>
    <hr>
    <div class="form">
        <div>
            <label for="fieldSimilar">Magnitud de hechizo similar: </label>
            <input type="number" id="fieldSimilar" name="fieldSimilar" bind:value={fieldSimilar} min=0 />
        </div>
        <div>
            <label for="fieldInestable">Niveles de inestabilidad: </label>
            <input type="number" id="fieldInestable" name="fieldInestable" bind:value={fieldInestable} min=0 max={data.teoriaMagica}/>
        </div>
        <div>
            <label for="fieldComponentes">Bono de componente: </label>
            <input type="number" id="fieldComponentes" name="fieldComponentes" bind:value={fieldComponentes} min=0 max={data.teoriaMagica}/>
        </div>
    </div>
    <h3>Total de laboratorio para hechizos: {totalHechizo}</h3>
    <hr>
    <h3>Parametros de hechizo: </h3>
    <div class="form">
        <div>
            <label for="fieldNivelBase">Nivel base: </label>
            <input type="number" id="fieldNivelBase" name="fieldNivelBase" bind:value={fieldNivelBase} min=0 max=4 />
        </div>
        <div>
            <label for="fieldAlcance">Magnitud del alcance: </label>
            <input type="number" id="fieldAlcance" name="fieldAlcance" bind:value={fieldAlcance} min=0 />
        </div>
        <div>
            <label for="fieldDuracion">Magnitud de la duración: </label>
            <input type="number" id="fieldDuracion" name="fieldDuracion" bind:value={fieldDuracion} min=0 />
        </div>
        <div>
            <label for="checkObjetivo">¿Tiene un objetivo?: </label>
            <input type="checkbox" id="checkObjetivo" name="checkObjetivo" bind:checked={checkObjetivo}>
        </div>
        <div>
            <label for="checkSentido">¿Afecta a un sentido?: </label>
            <input type="checkbox" id="checkSentido" name="checkSentido" bind:checked={checkSentido}>
        </div>
        {#if checkObjetivo}
            <div>
                <label for="fieldObjetivo">Objetivo: </label>
                <input type="number" id="fieldObjetivo" name="fieldObjetivo" bind:value={fieldObjetivo} min=0 />
            </div>
            <div>
                <label for="fieldMultiplicadorObjetivo">Multiplicador del objetivo: </label>
                <input type="number" id="fieldMultiplicadorObjetivo" name="fieldMultiplicadorObjetivo" bind:value={fieldTamano} min=1 />
            </div>
        {/if}
        {#if checkSentido}
            <div>
                <label for="fieldSentido">Magnitud del sentido: </label>
                <input type="number" id="fieldSentido" name="fieldSentido" bind:value={fieldSentido} min=0 />
            </div>
        {/if}
    </div>
    <h3>Nivel del hechizo: {nivelHechizo}</h3>
    {#if totalHechizo - nivelHechizo > 0}
        <h3>Se tardan: {Math.ceil(nivelHechizo / (totalHechizo - nivelHechizo))}</h3>
    {:else}
        <h3>No se puede crear el hechizo. Faltan {nivelHechizo-totalHechizo} puntos de total de Laboratorio.</h3>
    {/if}
</body>

<style>
    hr {
        width: 50%;
        margin: 10px auto;
    }
    *{
        margin-left: auto;
        margin-right: auto;
    }
    .form{
        display: flex;
        flex-direction: column;
        flex-flow: column;
        justify-content: center;
    }
    label{
        text-align: left;
        display: inline-block;
        width: 300px;
    }
    input{
        max-width: 45px;
        max-height: 30px;
        text-align: center;
    }
    div {
        margin-bottom: 15px;
    }
</style>