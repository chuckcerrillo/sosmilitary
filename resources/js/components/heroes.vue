<template>
    <div>
        <h1 class="text-center text-2xl text-gray-800 font-bold mb-8">Heroes</h1>
        <div class="flex items-center justify-center">



            <div
                v-for="(type,index,num) in types"
                class="flex-col p-1 text-gray-700"
            >
                <div class="text-center">{{ type.name }}</div>
                <div
                    class="rounded w-64 h-64 border border-gray-400 bg-gray-300 items-center flex justify-center"
                >
                    <div class="text-gray-500 text-center">Choose hero...</div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "heroes",
    data() {
        return {
            types: {
                brawler: {
                    name: 'Brawler',
                    type: 'infantry',
                },
                marksman: {
                    name: 'Marksman',
                    type: 'hunter',
                },
                scout: {
                    name: 'Scout',
                    type: 'rider',
                }
            }
            ,
            heroes: {
                General: [
                    {
                        name: 'march-slots',
                        display: 'March Slots',
                        type: 'general',
                    },
                    {
                        name: 'march-capacity',
                        display: 'March Capacity',
                        type: 'general',
                    },
                    {
                        name: 'training-capacity',
                        display: 'Training Capacity',
                        type: 'general',
                    },
                    {
                        name: 'training-speed',
                        display: 'Training Speed',
                        type: 'general',
                    },
                ],
                Troop: [
                    {
                        name: 'troop-attack',
                        display: 'Troop Attack',
                        type: 'troop',
                    },
                    {
                        name: 'troop-defense',
                        display: 'Troop Defense',
                        type: 'troop',
                    },
                    {
                        name: 'troop-lethality',
                        display: 'Troop Damage',
                        type: 'troop',
                    },
                    {
                        name: 'troop-health',
                        display: 'Troop Health',
                        type: 'troop',
                    },
                ],
                Infantry: [
                    {
                        name: 'infantry-attack',
                        display: 'Infantry Attack',
                        type: 'infantry',
                    },
                    {
                        name: 'infantry-defense',
                        display: 'Infantry Defense',
                        type: 'infantry',
                    },
                    {
                        name: 'infantry-lethality',
                        display: 'Infantry Lethality',
                        type: 'infantry',
                    },
                    {
                        name: 'infantry-health',
                        display: 'Infantry Health',
                        type: 'infantry',
                    },
                ],
                Hunter: [
                    {
                        name: 'hunter-attack',
                        display: 'Hunter Attack',
                        type: 'hunter',
                    },
                    {
                        name: 'hunter-defense',
                        display: 'Hunter Defense',
                        type: 'hunter',
                    },
                    {
                        name: 'hunter-lethality',
                        display: 'Hunter Lethality',
                        type: 'hunter',
                    },
                    {
                        name: 'hunter-health',
                        display: 'Hunter Health',
                        type: 'hunter',
                    },
                ],
                Rider: [
                    {
                        name: 'rider-attack',
                        display: 'Rider Attack',
                        type: 'rider',
                    },
                    {
                        name: 'rider-defense',
                        display: 'Rider Defense',
                        type: 'rider',
                    },
                    {
                        name: 'rider-lethality',
                        display: 'Rider Lethality',
                        type: 'rider',
                    },
                    {
                        name: 'rider-health',
                        display: 'Rider Health',
                        type: 'rider',
                    },
                ],
                Settlement: [
                    {
                        name: 'settlement-attack',
                        display: 'Settlement Army Attack',
                        type: 'settlement',
                    },
                    {
                        name: 'settlement-defense',
                        display: 'Settlement Army Defense',
                        type: 'settlement',
                    },
                    {
                        name: 'settlement-lethality',
                        display: 'Settlement Troop Lethality',
                        type: 'settlement',
                    },
                    {
                        name: 'settlement-health',
                        display: 'Settlement Troop Health',
                        type: 'settlement',
                    },
                ]
            }
        }
    }
}
</script>

<style scoped>

</style>
