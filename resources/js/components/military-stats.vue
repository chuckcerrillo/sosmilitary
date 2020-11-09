<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold">Military Stats</h1>
        <div class="text-xs my-2">
            <p>These are the stats that you will find in your stats screen. You can get there by opening your chief and choosing "stats" from the bottom menu. Once in the chief profile, scroll down to the "Military" section.</p>
        </div>

        <div class="flex flex-wrap items-center justify-center">

            <div
                v-for="(types,index,num) in stats"
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
            stats: {
                General: [
                    {
                        name: 'march-slots',
                        display: 'March Slots',
                    },
                    {
                        name: 'march-capacity',
                        display: 'March Capacity',
                    },
                    {
                        name: 'training-capacity',
                        display: 'Training Capacity',
                    },
                    {
                        name: 'training-speed',
                        display: 'Training Speed',
                    },
                ],
                Troop: [
                    {
                        name: 'troop-attack',
                        display: 'Troop Attack',
                    },
                    {
                        name: 'troop-defense',
                        display: 'Troop Defense',
                    },
                    {
                        name: 'troop-lethality',
                        display: 'Troop Damage',
                    },
                    {
                        name: 'troop-health',
                        display: 'Troop Health',
                    },
                ],
                Infantry: [
                    {
                        name: 'infantry-attack',
                        display: 'Infantry Attack',
                    },
                    {
                        name: 'infantry-defense',
                        display: 'Infantry Defense',
                    },
                    {
                        name: 'infantry-lethality',
                        display: 'Infantry Lethality',
                    },
                    {
                        name: 'infantry-health',
                        display: 'Infantry Health',
                    },
                ],
                Hunter: [
                    {
                        name: 'hunter-attack',
                        display: 'Hunter Attack',
                    },
                    {
                        name: 'hunter-defense',
                        display: 'Hunter Defense',
                    },
                    {
                        name: 'hunter-lethality',
                        display: 'Hunter Lethality',
                    },
                    {
                        name: 'hunter-health',
                        display: 'Hunter Health',
                    },
                ],
                Rider: [
                    {
                        name: 'rider-attack',
                        display: 'Rider Attack',
                    },
                    {
                        name: 'rider-defense',
                        display: 'Rider Defense',
                    },
                    {
                        name: 'rider-lethality',
                        display: 'Rider Lethality',
                    },
                    {
                        name: 'rider-health',
                        display: 'Rider Health',
                    },
                ],
                Settlement: [
                    {
                        name: 'settlement-attack',
                        display: 'Settlement Army Attack',
                    },
                    {
                        name: 'settlement-defense',
                        display: 'Settlement Army Defense',
                    },
                    {
                        name: 'settlement-lethality',
                        display: 'Settlement Troop Lethality',
                    },
                    {
                        name: 'settlement-health',
                        display: 'Settlement Troop Health',
                    },
                ]
            }
        }
    }
}
</script>

<style scoped>

</style>
