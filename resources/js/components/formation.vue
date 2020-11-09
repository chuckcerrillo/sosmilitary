<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold">Formation</h1>
        <div class="text-xs my-2">
            <p>This is the troop formation you'll be using in a march. Choose the appropriate heroes and troops for the activity you wish to do. For instance when attacking settlements you might want to use "Siege" heroes, etc.</p>
        </div>
        <div class="flex items-center justify-center">



            <div
                v-for="(type,index,num) in types"
                class="flex-col p-1 text-gray-700"
            >
                <div class="text-center">{{ type.name }}</div>
                <div
                    class="rounded w-32 h-32 border border-gray-400 bg-gray-300 items-center flex justify-center"
                    :class="data.captain === type.type ? 'border-blue-400':''"
                >
                    <div class="text-gray-500 text-center">Choose hero...</div>
                </div>
                <div v-if="data.captain === type.type"
                     class="text-sm p-2 text-center text-blue-400 font-bold">
                    Captain
                </div>
                <div v-else class="text-sm p-2 text-center text-gray-600 hover:text-blue-400 hover:underline cursor-pointer" @click="data.captain = type.type">Make captain</div>

            </div>

        </div>
        <h1 class="text-center text-2xl text-gray-800 font-bold my-4">Troops</h1>
        <div class="flex items-start justify-center">
            <div>
                <div>
                    <div>Plasma Level</div>
                    <div class="flex items-center justify-start">
                        <div
                            v-for="level in [0,1,2,3]"
                            class="p-2 m-2 text-2xl border border-gray-400 rounded w-12 h-12 text-center bg-gray-300 hover:border-blue-400 cursor-pointer"
                            :class="data.plasma === level ? 'border-blue-400 text-blue-600 bg-blue-200' : ''"
                            @click="data.plasma = level"
                        >
                            <div>{{"*".repeat(level)}}</div>
                        </div>
                    </div>

                </div>
                <div>
                    <div class="flex p-1 text-xs">
                        <div class="p-1 w-8">Tier</div>
                        <div class="p-1 w-28">Name</div>
                        <div class="p-1 w-16">Type</div>
                        <div class="p-1 w-16 text-right">Attack</div>
                        <div class="p-1 w-16 text-right">Defense</div>
                        <div class="p-1 w-16 text-right">Lethality</div>
                        <div class="p-1 w-16 text-right">Health</div>
                        <div class="p-1 w-20">Quantity</div>
                    </div>
                </div>

                <div
                    v-for="tier in [9,8,7,6,5,4,3,2,1,0]"
                >
                    <div
                        v-for="(troop,index) in ['Infantry','Rider','Hunter']"
                        class="flex p-1 text-sm items-center"
                    >
                        <div class="p-1 w-8 text-right">T{{tier+1}}</div>
                        <div class="p-1 w-28">{{troops[troop][tier].name}}</div>
                        <div class="p-1 w-16">{{troops[troop][tier].stats.type}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.plasma,'attack',troops[troop][tier])}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.plasma,'defense',troops[troop][tier])}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.plasma,'lethality',troops[troop][tier])}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.plasma,'health',troops[troop][tier])}}</div>
                        <div class="p-1 w-20"><input type="number" class="w-20 border border-gray-400 rounded p-1 text-xs" v-model="data.quantity[troop][tier]" /></div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: "formation",
    data() {
        return {
            data: {
                captain: 'infantry',
                plasma: 0,
                quantity: {
                    Infantry: [
                        0,0,0,0,0,0,0,0,0,0
                    ],
                    Hunter: [
                        0,0,0,0,0,0,0,0,0,0
                    ],
                    Rider: [
                        0,0,0,0,0,0,0,0,0,0
                    ],
                }
            },
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
            },
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
            },
            troops: {
                Infantry: [
                    {
                        tier: 1,
                        name: 'Grunt',
                        stats: {
                            health: 6,
                            attack: 1,
                            defense: 4,
                            lethality: 1,
                            type: 'Shields',
                            bp: 3,
                            load: 108,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 1,
                            },
                            3 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 1,
                            },
                        }
                    },
                    {
                        tier: 2,
                        name: 'Heavies',
                        stats: {
                            health: 7,
                            attack: 2,
                            defense: 5,
                            lethality: 2,
                            type: 'Shotguns',
                            bp: 4,
                            load: 124,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 1,
                            },
                            3 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 1,
                            },
                        }
                    },
                    {
                        tier: 3,
                        name: 'Rushers',
                        stats: {
                            health: 8,
                            attack: 3,
                            defense: 6,
                            lethality: 3,
                            type: 'Shields',
                            bp: 6,
                            load: 142,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 1,
                                defense: 0,
                            },
                            2 : {
                                attack: 0,
                                lethality: 0,
                                health: 2,
                                defense: 1,
                            },
                            3 : {
                                attack: 0,
                                lethality: 0,
                                health: 3,
                                defense: 1,
                            },
                        }
                    },
                    {
                        tier: 4,
                        name: 'Blasters',
                        stats: {
                            health: 9,
                            attack: 4,
                            defense: 7,
                            lethality: 4,
                            type: 'Shotguns',
                            bp: 10,
                            load: 164,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 0,
                                lethality: 0,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 0,
                                lethality: 0,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 5,
                        name: 'Blasters',
                        stats: {
                            health: 10,
                            attack: 5,
                            defense: 8,
                            lethality: 5,
                            type: 'Shields',
                            bp: 14,
                            load: 188,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 0,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 1,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 3,
                                lethality: 2,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 6,
                        name: 'Survivalists',
                        stats: {
                            health: 11,
                            attack: 6,
                            defense: 9,
                            lethality: 6,
                            type: 'Shotguns',
                            bp: 21,
                            load: 217,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 0,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 1,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 3,
                                lethality: 2,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 7,
                        name: 'Hackers',
                        stats: {
                            health: 12,
                            attack: 7,
                            defense: 10,
                            lethality: 7,
                            type: 'Shields',
                            bp: 30,
                            load: 249,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 0,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 1,
                                health: 2,
                                defense: 3,
                            },
                            3 : {
                                attack: 3,
                                lethality: 2,
                                health: 3,
                                defense: 4,
                            },
                        }
                    },
                    {
                        tier: 8,
                        name: 'Guerillas',
                        stats: {
                            health: 13,
                            attack: 8,
                            defense: 11,
                            lethality: 8,
                            type: 'Shotguns',
                            bp: 41,
                            load: 287,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 0,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 1,
                                health: 2,
                                defense: 3,
                            },
                            3 : {
                                attack: 3,
                                lethality: 2,
                                health: 3,
                                defense: 4,
                            },
                        }
                    },
                    {
                        tier: 9,
                        name: 'Maulers',
                        stats: {
                            health: 14,
                            attack: 9,
                            defense: 12,
                            lethality: 9,
                            type: 'Shields',
                            bp: 54,
                            load: 330,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 0,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 1,
                                health: 2,
                                defense: 3,
                            },
                            3 : {
                                attack: 3,
                                lethality: 2,
                                health: 3,
                                defense: 4,
                            },
                        }
                    },
                    {
                        tier: 10,
                        name: 'Executioners',
                        stats: {
                            health: 15,
                            attack: 10,
                            defense: 13,
                            lethality: 10,
                            type: 'Shotguns',
                            bp: 71,
                            load: 379,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 0,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 1,
                                health: 2,
                                defense: 3,
                            },
                            3 : {
                                attack: 3,
                                lethality: 2,
                                health: 3,
                                defense: 4,
                            },
                        }
                    },
                ],
                Hunter: [
                    {
                        tier: 1,
                        name: 'Archers',
                        stats: {
                            health: 1,
                            attack: 5,
                            defense: 1,
                            lethality: 6,
                            type: 'Bows',
                            bp: 3,
                            load: 108,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 2,
                        name: 'Rifles',
                        stats: {
                            health: 2,
                            attack: 6,
                            defense: 2,
                            lethality: 7,
                            type: 'Snipers',
                            bp: 4,
                            load: 124,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 3,
                        name: 'Shooters',
                        stats: {
                            health: 3,
                            attack: 7,
                            defense: 3,
                            lethality: 8,
                            type: 'Snipers',
                            bp: 6,
                            load: 142,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 3,
                                lethality: 3,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 4,
                        name: 'Trackers',
                        stats: {
                            health: 4,
                            attack: 8,
                            defense: 4,
                            lethality: 9,
                            type: 'Bows',
                            bp: 10,
                            load: 164,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 3,
                                lethality: 3,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 5,
                        name: 'Crossbows',
                        stats: {
                            health: 5,
                            attack: 9,
                            defense: 5,
                            lethality: 10,
                            type: 'Bows',
                            bp: 14,
                            load: 188,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 3,
                                lethality: 3,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 6,
                        name: 'Marksmen',
                        stats: {
                            health: 6,
                            attack: 10,
                            defense: 6,
                            lethality: 11,
                            type: 'Snipers',
                            bp: 21,
                            load: 217,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 3,
                                lethality: 3,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 7,
                        name: 'Sharpshooters',
                        stats: {
                            health: 7,
                            attack: 11,
                            defense: 7,
                            lethality: 12,
                            type: 'Snipers',
                            bp: 30,
                            load: 249,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 8,
                        name: 'Hawks',
                        stats: {
                            health: 8,
                            attack: 12,
                            defense: 8,
                            lethality: 13,
                            type: 'Bows',
                            bp: 41,
                            load: 287,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 9,
                        name: 'Nightstalkers',
                        stats: {
                            health: 9,
                            attack: 13,
                            defense: 9,
                            lethality: 14,
                            type: 'Bows',
                            bp: 54,
                            load: 330,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 10,
                        name: 'Nightstalkers',
                        stats: {
                            health: 10,
                            attack: 14,
                            defense: 10,
                            lethality: 15,
                            type: 'Snipers',
                            bp: 71,
                            load: 379,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 1,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 2,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 3,
                                defense: 3,
                            },
                        }
                    },
                ],
                Rider: [
                    {
                        tier: 1,
                        name: 'Rovers',
                        stats: {
                            health: 2,
                            attack: 4,
                            defense: 2,
                            lethality: 5,
                            type: 'ATVs',
                            bp: 3,
                            load: 108,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 2,
                        name: 'Scramblers',
                        stats: {
                            health: 3,
                            attack: 5,
                            defense: 3,
                            lethality: 6,
                            type: 'Bikers',
                            bp: 4,
                            load: 124,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 0,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 1,
                                lethality: 0,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 3,
                        name: 'Angels',
                        stats: {
                            health: 4,
                            attack: 6,
                            defense: 4,
                            lethality: 7,
                            type: 'Bikers',
                            bp: 6,
                            load: 142,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 2,
                                lethality: 3,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 4,
                        name: 'Skirmishers',
                        stats: {
                            health: 5,
                            attack: 7,
                            defense: 5,
                            lethality: 8,
                            type: 'ATVs',
                            bp: 10,
                            load: 164,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 0,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 0,
                                defense: 0,
                            },
                            3 : {
                                attack: 3,
                                lethality: 3,
                                health: 0,
                                defense: 0,
                            },
                        }
                    },
                    {
                        tier: 5,
                        name: 'Hogs',
                        stats: {
                            health: 6,
                            attack: 8,
                            defense: 6,
                            lethality: 9,
                            type: 'Bikers',
                            bp: 14,
                            load: 188,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 1,
                                defense: 2,
                            },
                            3 : {
                                attack: 3,
                                lethality: 3,
                                health: 2,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 6,
                        name: 'Rangers',
                        stats: {
                            health: 7,
                            attack: 9,
                            defense: 7,
                            lethality: 10,
                            type: 'ATVs',
                            bp: 21,
                            load: 217,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 1,
                            },
                            2 : {
                                attack: 2,
                                lethality: 2,
                                health: 1,
                                defense: 2,
                            },
                            3 : {
                                attack: 3,
                                lethality: 3,
                                health: 2,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 7,
                        name: 'Raiders',
                        stats: {
                            health: 8,
                            attack: 10,
                            defense: 11,
                            lethality: 8,
                            type: 'ATV',
                            bp: 30,
                            load: 249,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 1,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 2,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 8,
                        name: 'Banshees',
                        stats: {
                            health: 9,
                            attack: 11,
                            defense: 9,
                            lethality: 12,
                            type: 'Bikers',
                            bp: 41,
                            load: 287,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 1,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 2,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 9,
                        name: 'Demon Raiders',
                        stats: {
                            health: 10,
                            attack: 12,
                            defense: 10,
                            lethality: 13,
                            type: 'ATVs',
                            bp: 54,
                            load: 330,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 1,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 2,
                                defense: 3,
                            },
                        }
                    },
                    {
                        tier: 10,
                        name: 'Death Cruisers',
                        stats: {
                            health: 11,
                            attack: 13,
                            defense: 11,
                            lethality: 14,
                            type: 'Bikers',
                            bp: 71,
                            load: 379,
                            speed: 11,
                        },
                        plasma: {
                            1 : {
                                attack: 1,
                                lethality: 1,
                                health: 0,
                                defense: 1,
                            },
                            2 : {
                                attack: 3,
                                lethality: 2,
                                health: 1,
                                defense: 2,
                            },
                            3 : {
                                attack: 4,
                                lethality: 3,
                                health: 2,
                                defense: 3,
                            },
                        }
                    },
                ]
            }
        }
    },
    methods: {
        getPlasma(level,type,stats){
            let offset = 0;
            if(level > 0)
            {
                offset = stats.plasma[level][type];
                console.log('offset');
                console.log(offset);
            }

            return stats.stats[type] + offset;
        }
    }
}
</script>

<style scoped>

</style>
