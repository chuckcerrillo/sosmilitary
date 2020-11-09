<template>
    <div class="text-gray-200 relative">
        <h1 class="text-center text-2xl font-bold mb-2">Summary</h1>
        <div class="flex flex-wrap items-center justify-center mb-4">

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Attack
                </div>
                <div class="text-3xl font-bold">
                    0.0
                </div>
            </div>

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Defense
                </div>
                <div class="text-3xl font-bold">
                    0.0
                </div>
            </div>

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Lethality
                </div>
                <div class="text-3xl font-bold">
                    0.0
                </div>
            </div>

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Health
                </div>
                <div class="text-3xl font-bold">
                    0.0
                </div>
            </div>

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Total Attack Power
                </div>
                <div class="text-3xl font-bold">
                    0.0
                </div>
            </div>

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Total Defense Power
                </div>
                <div class="text-3xl font-bold">
                    0.0
                </div>
            </div>
        </div>
        <div class="text-center font-bold text">
            <div v-if="showSummary" class="hover:text-green-400 cursor-pointer" @click="toggleSummary()">
                Hide detailed breakdown
            </div>
            <div v-else class="hover:text-green-400 cursor-pointer" @click="toggleSummary()">
                Show detailed breakdown
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "summary",
    props: [
        'showSummary'
    ],
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
    },
    methods: {
        toggleSummary() {
            this.$emit('toggleSummary');
        }
    }
}
</script>

<style scoped>

</style>
