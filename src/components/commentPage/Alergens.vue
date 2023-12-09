<template>
    <div class="alergens-box">
        <div @click="show = !show" class="toggle-alergens">
            <h3>Alergény</h3>
            <img src="@/assets/images/drop-down-arrow.png" alt="arrow">
        </div>
        <Transition name="slide">
            <div v-if="show">
                <ol>
                    <li>Obilniny obsahujúce lepok (t.j. pšenica, raž, jačmeň, ovos, špalda, kamut alebo ich hybridné odrody).</li>
                    <li>Kôrovce a výrobky z nich.</li>
                    <li>Vajcia a výrobky z nich.</li>
                    <li>Ryby a výrobky z nich.</li>
                    <li>Arašidy a výrobky z nich.</li>
                    <li>Sójové zrná a výrobky z nich.</li>
                    <li>Mlieko a výrobky z neho.</li>
                    <li>Orechy, ktorými sú mandle, lieskové orechy, vlašské orechy, kešu, pekanové orechy, para orechy, pistácie, makadamové orechy a queenslandské orechy a výrobky z nich.</li>
                    <li>Zeler a výrobky z neho.</li>
                    <li>Horčica a výrobky z nej.</li>
                    <li>Sezamové semená a výrobky z nich.</li>
                    <li>Oxid siričitý a siričitany v koncentráciách vyšších ako 10 mg/kg alebo 10 mg/l. /konzervanty/</li>
                    <li>Vlčí bob a výrobky z neho.</li>
                    <li>Mäkkýše a výrobky z nich.</li>
                </ol>
            </div>
        </Transition>
    </div>
</template>

<script>
export default {
  name: 'Alergens',
  data() {
    return {
        show: false
    }
  },
}
</script>
