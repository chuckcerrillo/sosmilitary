<template>
    <div class="flex-col flex-1 h-screen overflow-y-hidden bg-gray-200 relative">
        <div class="w-full bg-gray-800 text-white h-32">
            <div class="text-3xl font-bold p-4 tracking-tighter">State of Survival - Military Calculator</div>
        </div>
        <div class="overflow-y-auto fixed inset-x-0 h-auto" style="top:8rem; bottom: 16rem;">
            <MilitaryStats class="border-b border-gray-400 py-8" />
            <Formation class="border-b border-gray-400 py-8" />
            <Heroes class="border-b border-gray-400 py-8" />
            <HeroGear class="border-b border-gray-400 py-8" />
        </div>
        <div class="fixed z-10 bottom-0 inset-x-0 bg-gray-800 text-white mb-24" :class="ui.showSummary ? 'h-128' : 'h-40'">
            <Summary
                v-on:toggleSummary="toggleSummary"
                :showSummary="ui.showSummary"
            />
        </div>
        <div class="fixed z-20 bottom-0 inset-x-0 w-full bg-black text-white h-24">
            <div class="p-4 text-gray-500 text-sm">SOS Military Calculator &copy; 2020 - Fan made by <a class="text-white hover:underline" href="https://www.cerriscapades.com/">Cerriscapades</a>. No affiliation with KingsGroup.</div>
        </div>
    </div>
</template>

<script>
import MilitaryStats from '../components/military-stats'
import Heroes from '../components/heroes'
import Formation from '../components/formation'
import HeroGear from '../components/hero-gear'
import Summary from '../components/summary'

export default {
    name: "App",
    components: {
        MilitaryStats,
        Heroes,
        Formation,
        HeroGear,
        Summary
    },
    data() {
        return {
            ui : {
                showSummary: false,
            }
        }
    },
    methods: {
        toggleSummary() {
            this.ui.showSummary = !this.ui.showSummary;
        }
    }
}
</script>

<style scoped>

</style>
