<script>
    export let data;
    import CrearHechizo from "./CrearHechizo.svelte";

    let fieldPenalizadores = 0;
    let fieldAura = 0;
    let fieldCalidad = 0;
    let checkEspecializacion = false;
    let fieldBono = 0;
    let checkExperimentando = false;
    let fieldExperimentando = 0;
    let fieldBonoExperimentacion = 1;
    let fieldVis = 0;
    let checkMaterialesExtra = 0;
    let fieldTecnica = "creo";
    let fieldForma = "corpus";
    let totalLaboratorio;
    let viewportComponent;

    function calcularTotal(){
        totalLaboratorio = Number(data.tecnica[fieldTecnica]);
        totalLaboratorio += Number(data.forma[fieldForma]);
        totalLaboratorio += Number(data.inteligencia);
        totalLaboratorio += Number(data.teoriaMagica);
        totalLaboratorio += Number(fieldAura);
        totalLaboratorio += Number(fieldCalidad);
        if (checkEspecializacion) totalLaboratorio += 1;
        totalLaboratorio += Number(fieldBono);
        if (checkExperimentando){
            totalLaboratorio += Number(fieldExperimentando)
            totalLaboratorio += Number(fieldBonoExperimentacion);
            totalLaboratorio += Number(fieldVis*2);
        }else{
            totalLaboratorio += Number(fieldVis);
        }
        if (checkMaterialesExtra) totalLaboratorio += Number((Math.ceil(data.teoriaMagica / 2)));
        totalLaboratorio -= Number(fieldPenalizadores);
    }

    function cargarHechizo(){
        viewportComponent= CrearHechizo;
    }

    calcularTotal();

    $: fieldPenalizadores,  fieldAura, fieldCalidad, checkEspecializacion, fieldBono, checkExperimentando, fieldExperimentando, fieldBonoExperimentacion, fieldVis, checkMaterialesExtra, fieldTecnica, fieldForma, calcularTotal();
</script>

<body>
    <div class="form">
        <div>
            <label for="fieldTecnica">Tecnica: </label>
            <select id="fieldTecnica" name="fieldTecnica" required  bind:value={fieldTecnica} >
                <option value="creo">Creo</option>
                <option value="muto">Muto</option>
                <option value="intellego">Intellego</option>
                <option value="rego">Rego</option>
                <option value="perdo">Perdo</option>
            </select>
        </div>
        <div>
            <label for="fieldForma">Forma: </label>
            <select id="fieldForma" name="fieldForma" required  bind:value={fieldForma}>
                <option value="corpus">Corpus</option>
                <option value="herbam">Herbam</option>
                <option value="animal">Animal</option>
                <option value="ignem">Ignem</option>
                <option value="terram">Terram</option>
                <option value="auram">Auram</option>
                <option value="aquam">Aquam</option>
                <option value="imaginem">Imaginem</option>
                <option value="mentem">Mentem</option>
                <option value="vim">Vim</option>
            </select>
        </div>
        <div>
            <label for="fieldAura">Aura: </label>
            <input type="number" id="fieldAura" name="fieldAura" bind:value={fieldAura} required>
        </div>
        <div>
            <label for="fieldCalidad">Calidad del laboratorio: </label>
            <input type="number" id="fieldCalidad" name="fieldCalidad" bind:value={fieldCalidad} required>
        </div>
        <div>
            <label for="checkEspecializacion">¿Especialización del personaje?: </label>
            <input type="checkbox" id="checkEspecializacion" name="checkEspecializacion" bind:checked={checkEspecializacion}>
        </div>
        <div>
            <label for="fieldBono">Bonos: </label>
            <input type="number" id="fieldBono" name="fieldBono" bind:value={fieldBono} required min=0>
        </div>
        <div>
            <label for="checkExperimentando">¿Experimentando? </label>
            <input type="checkbox" id="checkExperimentando" name="checkExperimentando" bind:checked={checkExperimentando}>
        </div>
        {#if checkExperimentando}
            <div>
                <label for="fieldExperimentando">Riesgo de experimentación: </label>
                <input type="number" id="fieldExperimentando" name="fieldExperimentando" bind:value={fieldExperimentando} required min=0 max=3>
            </div>
            <div>
                <label for="fieldBonoExperimentacion">Bono de experimentación: </label>
                <input type="number" id="fieldBonoExperimentacion" name="fieldBonoExperimentacion" bind:value={fieldBonoExperimentacion} required min=1>
            </div>
        {/if}
        <div>
            <label for="fieldVis">Vis: </label>
            <input type="number" id="fieldVis" name="fieldVis" bind:value={fieldVis} required min=0 max={data.teoriaMagica*2}>
        </div>
        <div>
            <label for="fieldMaterialesExtra">Materiales Extra: </label>
            <input type="checkbox" id="fieldMaterialesExtra" name="fieldMaterialesExtra" bind:checked={checkMaterialesExtra} required>
        </div>
        <div>
            <label for="fieldPenalizadores">Penalizadores: </label>
            <input type="number" id="fieldPenalizadores" name="fieldPenalizadores" bind:value={fieldPenalizadores} required min=0>
        </div>
    </div>
    <h3>Total de laboratorio: {totalLaboratorio}</h3>
    <!-- Make a button than nests a component CrearHechizo and uses totalLaboratorio as argument -->
    <button on:click={cargarHechizo}>Crear Hechizo</button>
    <svelte:component this={viewportComponent} bind:totalLaboratorio={totalLaboratorio} bind:data={data}></svelte:component>
</body>


<style>
    hr {
        width: 50%;
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
        text-align: right;
        display: inline-block;
        width: 300px;
        text-align: left;
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