<template>
    <div>
        <h1 class="text-center text-2xl text-gray-800 font-bold mb-8">Military Stats</h1>
        <div class="flex items-center justify-center">

            <div
                v-for="(types,index,num) in stats"
                class="flex-col p-1 text-gray-700"
            >
                <div class="text-center">{{ index }} Bonuses</div>
                <div
                    v-for="stat in types"
                    class="flex p-1"
                    :class="num <= types.length ? 'pr-8':''"
                >
                    <div class="" :class="index == 'Settlement' ? 'w-56' : 'w-32'">{{stat.display}}</div>
                    <div><input class="p-1 border border-gray-400 rounded w-16 text-sm" type="text" /></div>
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
