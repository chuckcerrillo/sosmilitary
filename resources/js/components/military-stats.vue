<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold">Military Stats</h1>
        <div class="text-xs my-2">
            <p>These are the stats that you will find in your stats screen. You can get there by opening your chief and choosing "stats" from the bottom menu. Once in the chief profile, scroll down to the "Military" section.</p>
        </div>

        <div class="flex flex-wrap items-center justify-center">

            <div
                v-for="(types,index,num) in library.Military"
                class="flex-col p-1 text-gray-700"
            >
                <div class="tracking-tight text-center text-xl">{{ index }} Bonuses</div>
                <div
                    v-for="stat in types"
                    class="flex p-1 text-xs items-center"
                >
                    <div class="w-48">{{stat.display}}</div>
                    <div><input class="p-1 border border-gray-400 rounded w-16 text-sm" type="text" v-model="data[stat.name]" /></div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "military-stats",
    props: [
        'library',
    ],
    data() {
        return {
            data: {
                'march-slots': '0.0%',
                'march-capacity': '0.0%',
                'training-capacity': '0.0%',
                'training-speed': '0.0%',
                'troop-attack': '0.0%',
                'troop-defense': '0.0%',
                'troop-lethality': '0.0%',
                'troop-health': '0.0%',
                'infantry-attack': '0.0%',
                'infantry-defense': '0.0%',
                'infantry-lethality': '0.0%',
                'infantry-health': '0.0%',
                'hunter-attack': '0.0%',
                'hunter-defense': '0.0%',
                'hunter-lethality': '0.0%',
                'hunter-health': '0.0%',
                'rider-attack': '0.0%',
                'rider-defense': '0.0%',
                'rider-lethality': '0.0%',
                'rider-health': '0.0%',
                'settlement-attack': '0.0%',
                'settlement-defense': '0.0%',
                'settlement-lethality': '0.0%',
                'settlement-health': '0.0%',
            },

        }
    }
}
</script>

<style scoped>

</style>
