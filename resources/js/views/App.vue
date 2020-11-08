<template>
    <div class="flex flex-col flex-1 h-screen overflow-y-hidden bg-gray-200">
        <div class="w-full bg-gray-800 text-white h-32">TOP NAVIGATION</div>
        <div class="h-full">
            <MilitaryStats class="border-b border-gray-400 py-8" />
            <Heroes class="border-b border-gray-400 py-8" />
            <HeroGear class="border-b border-gray-400 py-8" />
        </div>
        <div class="w-full bg-gray-800 text-white h-32">FOOTER</div>
    </div>
</template>

<script>
import MilitaryStats from '../components/military-stats'
import Heroes from '../components/heroes'
import HeroGear from '../components/hero-gear'

export default {
    name: "App",
    components: {
        MilitaryStats,
        Heroes,
        HeroGear
    }
}
</script>

<style scoped>

</style>
