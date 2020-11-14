<template>
    <div class="flex-col flex-1 h-screen overflow-y-hidden bg-gray-200 relative">
        <div class="w-full bg-gray-800 text-white">
            <div class="text-2xl font-bold p-4 tracking-tighter">State of Survival - Military Calculator</div>
            <div class="flex items-center justify-center text-sm p-2">
                <a class="inline-block cursor-pointer rounded hover:bg-gray-600 hover:text-white p-2 px-8">My Stats</a>
                <a class="inline-block cursor-pointer rounded hover:bg-gray-600 hover:text-white p-2 px-8">Heroes</a>
                <a class="inline-block cursor-pointer rounded hover:bg-gray-600 hover:text-white p-2 px-8">Troop Formation</a>
                <a class="inline-block cursor-pointer rounded hover:bg-gray-600 hover:text-white p-2 px-8">Import/Export</a>
            </div>
        </div>
        <div class="overflow-y-auto fixed inset-x-0 h-auto" style="top:7.5rem; bottom: 16rem;">
            <MilitaryStats
                v-on:saveLocalStorage="saveLocalStorage"
                :library="library"
                :data="data"
                class="border-b border-gray-400 py-8"
            />
            <Formation
                v-on:selectHero="selectHero"
                v-on:saveLocalStorage="saveLocalStorage"
                :library="library"
                :data="data"
                class="border-b border-gray-400 py-8"
            />
            <Heroes
                v-on:saveLocalStorage="saveLocalStorage"
                :library="library"
                :data="data"
                class="border-b border-gray-400 py-8"
            />
            <HeroGear
                v-on:saveLocalStorage="saveLocalStorage"
                :library="library"
                :data="data"
                class="border-b border-gray-400 py-8"
            />
        </div>
        <div class="fixed z-10 bottom-0 inset-x-0 bg-gray-700 text-white mb-24" :class="ui.showSummary ? '' : 'h-40'" :style="ui.showSummary ? 'top: 7.5rem; bottom: 0;' : ''">
            <Summary
                v-on:toggleSummary="toggleSummary"
                :library="library"
                :data="data"
                :showSummary="ui.showSummary"
            />
        </div>
        <div class="fixed z-20 bottom-0 inset-x-0 w-full bg-black text-white h-24">
<!--            <button @click="saveLocalStorage()">Save</button>-->
<!--            <button @click="loadLocalStorage()">Load</button>-->
<!--            <button @click="checkLocalStorage()">Check</button>-->
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
            data: {
                Military: {
                    'march-slots': '1',
                    'march-capacity': '0',
                    'training-capacity': '0',
                    'training-speed': '0',
                    'troop-attack': '0',
                    'troop-defense': '0',
                    'troop-lethality': '0',
                    'troop-health': '0',
                    'infantry-attack': '0',
                    'infantry-defense': '0',
                    'infantry-lethality': '0',
                    'infantry-health': '0',
                    'hunter-attack': '0',
                    'hunter-defense': '0',
                    'hunter-lethality': '0',
                    'hunter-health': '0',
                    'rider-attack': '0',
                    'rider-defense': '0',
                    'rider-lethality': '0',
                    'rider-health': '0',
                    'settlement-attack': '0',
                    'settlement-defense': '0',
                    'settlement-lethality': '0',
                    'settlement-health': '0',
                },
                Formation: {
                    active: 0,
                    saved: [{
                        captain: 'infantry',
                        heroes: {
                            brawler: false,
                            marksman: false,
                            scout: false,
                        },
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
                    }]
                },
                Heroes: {
                    rusty: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    ghost: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    sarge: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    travis: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    mike: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    eva: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    tony: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    basel: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    candy: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    jane: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    chef: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    maddie: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    nikola: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    lucky: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    ray: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    wolfe: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    trish: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    jeb: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    ash: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    zoe: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                    miho: {
                        rank: 0,
                        upgrade: 1,
                        level: 1,
                    },
                },
                Summary: {
                    boosts: {
                        Troop: {
                            attack: 0,
                            defense: 0,
                            lethality: 0,
                            health: 0
                        },
                        Infantry: {
                            attack: 0,
                            defense: 0,
                            lethality: 0,
                            health: 0
                        },
                        Hunter: {
                            attack: 0,
                            defense: 0,
                            lethality: 0,
                            health: 0
                        },
                        Rider: {
                            attack: 0,
                            defense: 0,
                            lethality: 0,
                            health: 0
                        },
                        Settlement: {
                            attack: 0,
                            defense: 0,
                            lethality: 0,
                            health: 0
                        },
                        Enemy: {
                            attack: 0,
                            defense: 0,
                            lethality: 0,
                            health: 0
                        },
                    }
                },
                HeroGear: {
                    brawler: {
                        helmet: {
                            tier: 2,
                            step: 2,
                        },
                        chest: {
                            tier: 3,
                            step: 2,
                        },
                        feet: {
                            tier: 4,
                            step: 2,
                        },
                    },
                    marksman: {
                        helmet: {
                            tier: 1,
                            step: 1,
                        },
                        chest: {
                            tier: 1,
                            step: 1,
                        },
                        feet: {
                            tier: 1,
                            step: 1,
                        },
                    },
                    scout: {
                        helmet: {
                            tier: 1,
                            step: 1,
                        },
                        chest: {
                            tier: 1,
                            step: 1,
                        },
                        feet: {
                            tier: 1,
                            step: 1,
                        },
                    }
                }
            },
            ui : {
                showSummary: false,
            },
            library: {
                Heroes: {
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
                    ranks: [
                        {
                            name: 'Cadet',
                            levels: 5,
                        },
                        {
                            name: '2nd Lieutenant',
                            levels: 5,
                        },
                        {
                            name: '1st Lieutenant',
                            levels: 5,
                        },
                        {
                            name: 'Captain',
                            levels: 5,
                        },
                        {
                            name: 'Major',
                            levels: 5,
                        },
                        {
                            name: 'Lt. Colonel',
                            levels: 5,
                        },
                        {
                            name: 'Colonel',
                            levels: 5,
                        },
                        {
                            name: 'General',
                            levels: 1,
                        },
                    ],
                    heroes: [
                        {
                            key: 'rusty',
                            name: 'Rusty',
                            type: 'brawler',
                            rarity: 'epic',
                            stats: {
                                base: {
                                    attack: '97.75',
                                    defense: '97.75',
                                },
                            },
                        },
                        {
                            key: 'ghost',
                            name: 'Ghost',
                            type: 'scout',
                            rarity: 'epic',
                            stats: {
                                base: {
                                    attack: '97.75',
                                    defense: '97.75',
                                },
                            },
                        },
                        {
                            key: 'sarge',
                            name: 'Sarge',
                            type: 'marksman',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                                infected: {
                                    defense: '65.2',
                                },
                            },
                        },
                        {
                            key: 'travis',
                            name: 'Travis',
                            type: 'scout',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '104.25',
                                    defense: '104.25',
                                },
                                infected: {
                                    lethality: '65.2',
                                },
                            },
                        },
                        {
                            key: 'mike',
                            name: 'Mike',
                            type: 'marksman',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                            },
                        },
                        {
                            key: 'eva',
                            name: 'Eva',
                            type: 'marksman',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                                enemy: {
                                    health: '-19.5',
                                },
                            },
                        },
                        {
                            key: 'tony',
                            name: 'Tony',
                            type: 'scout',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                                infected: {
                                    defense: '65.2',
                                },
                            },
                        },
                        {
                            key: 'basel',
                            name: 'Basel',
                            type: 'scout',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                                infected: {
                                    health: '65.2',
                                },
                            },
                        },
                        {
                            key: 'candy',
                            name: 'Candy',
                            type: 'scout',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                                infected: {
                                    defense: '65.2',
                                },
                            },
                        },
                        {
                            key: 'jane',
                            name: 'Jane',
                            type: 'scout',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                                infected: {
                                    health: '65.2',
                                },
                            },
                        },
                        {
                            key: 'chef',
                            name: 'Chef',
                            type: 'brawler',
                            rarity: 'elite',
                            stats: {
                                base: {
                                    attack: '130.3',
                                    defense: '130.3',
                                },
                            },
                        },
                        {
                            key: 'maddie',
                            name: 'Maddie and Frank',
                            type: 'scout',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '211.75',
                                    defense: '211.75',
                                },
                                settlement: {
                                    attack: '63.5',
                                },
                                rally: {
                                    attack: '21.15',
                                },
                            },
                        },
                        {
                            key: 'nikola',
                            name: 'Nikola',
                            type: 'brawler',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '211.75',
                                    defense: '211.75',
                                },
                                infected: {
                                    attack: '105.9',
                                },
                                rally: {
                                    defense: '21.15',
                                },
                            },
                        },
                        {
                            key: 'lucky',
                            name: 'Lucky',
                            type: 'marksman',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '201.15',
                                    defense: '201.15',
                                },
                                enemy: {
                                    attack: '-31.8',
                                },
                                rally: {
                                    health: '21.15',
                                },
                            },
                        },
                        {
                            key: 'ray',
                            name: 'Ray and Rolex',
                            type: 'brawler',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '222.35',
                                    defense: '222.35',
                                },
                                enemy: {
                                    attack: '-31.8',
                                },
                                settlement: {
                                    health: '63.5',
                                },
                            },
                        },
                        {
                            key: 'wolfe',
                            name: 'Wolfe',
                            type: 'brawler',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '222.35',
                                    defense: '222.35',
                                },
                                settlement: {
                                    health: '63.5',
                                },
                                rally: {
                                    lethality: '21.15',
                                },
                            },
                        },
                        {
                            key: 'trish',
                            name: 'Trish',
                            type: 'scout',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '216',
                                    defense: '216',
                                },
                                settlement: {
                                    lethality: '63.5',
                                },
                                enemy: {
                                    attack: '-31.8',
                                },
                            },
                        },
                        {
                            key: 'jeb',
                            name: 'Jeb',
                            type: 'marksman',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '233.45',
                                    defense: '233.45',
                                },
                                rally: {
                                    attack: '21.15',
                                },
                                enemy: {
                                    lethality: '-31.8',
                                },
                            },
                        },
                        {
                            key: 'ash',
                            name: 'Ash',
                            type: 'brawler',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '320.05',
                                    defense: '320.05',
                                },
                                settlement: {
                                    attack: '63.5',
                                },
                                enemy: {
                                    def: '-31.8',
                                },
                            },
                        },
                        {
                            key: 'zoe',
                            name: 'Zoe',
                            type: 'marksman',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '320.05',
                                    defense: '320.05',
                                },
                                settlement: {
                                    defense: '63.5',
                                },
                                rally: {
                                    defense: '21.15',
                                },
                            },
                        },
                        {
                            key: 'miho',
                            name: 'Miho',
                            type: 'scout',
                            rarity: 'legendary',
                            stats: {
                                base: {
                                    attack: '315.05',
                                    defense: '315.05',
                                },
                                enemy: {
                                    health: '-31.8',
                                },
                                rally: {
                                    health: '21.15',
                                },
                            },
                        },
                    ],
                    march: [
                        65,
                        140,
                        220,
                        305,
                        400,
                        500,
                        605,
                        720,
                        840,
                        970,
                        1100,
                        1240,
                        1390,
                        1540,
                        1700,
                        1870,
                        2040,
                        2225,
                        2410,
                        2605,
                        2805,
                        3010,
                        3225,
                        3445,
                        3670,
                        3905,
                        4145,
                        4390,
                        4645,
                        4905,
                        5175,
                        5445,
                        5725,
                        6015,
                        6310,
                        6600,
                        6895,
                        7190,
                        7480,
                        7775,
                        8070,
                        8365,
                        8655,
                        8950,
                        9245,
                        9540,
                        9830,
                        10125,
                        10420,
                        10685,
                        10925,
                        11140,
                        11340,
                        11525,
                        11700,
                        11860,
                        12010,
                        12140,
                        12260,
                        12370,
                        12470,
                        12560,
                        12650,
                        12370,
                        12800,
                        12870,
                        12930,
                        12980,
                        13030,
                        13070,
                        13110,
                        13150,
                        13190,
                        13230,
                        13270,
                        13310,
                        13350,
                        13390,
                        13430,
                        13470,
                    ],
                    scales: {
                        '-31.8' : [
                            -3.5,
                            -4,
                            -4.5,
                            -5,
                            -5.5,
                            -6,
                            -6.6,
                            -7.2,
                            -7.7,
                            -8.3,
                            -8.9,
                            -9.5,
                            -10.2,
                            -10.8,
                            -11.4,
                            -12.1,
                            -12.8,
                            -13.6,
                            -14.4,
                            -15.1,
                            -15.9,
                            -16.8,
                            -17.8,
                            -18.7,
                            -19.7,
                            -20.6,
                            -21.7,
                            -22.7,
                            -23.7,
                            -24.7,
                            -25.7,
                            -26.9,
                            -28.1,
                            -29.3,
                            -30.6,
                            -31.8,
                        ],
                        '-19.5' : [
                            -1.6,
                            -1.9,
                            -2.3,
                            -2.6,
                            -3,
                            -3.3,
                            -3.7,
                            -4.1,
                            -4.5,
                            -4.9,
                            -5.3,
                            -5.7,
                            -6.1,
                            -6.6,
                            -7,
                            -7.4,
                            -7.9,
                            -8.4,
                            -8.8,
                            -9.3,
                            -9.8,
                            -10.4,
                            -10.9,
                            -11.5,
                            -12.1,
                            -12.7,
                            -13.3,
                            -14,
                            -14.6,
                            -15.2,
                            -15.8,
                            -16.6,
                            -17.3,
                            -18.1,
                            -18.8,
                            -19.5,
                        ],
                        '21.15' : [
                            2.35,
                            2.65,
                            3,
                            3.35,
                            3.7,
                            4,
                            4.4,
                            4.8,
                            5.15,
                            5.55,
                            5.95,
                            6.35,
                            6.8,
                            7.2,
                            7.6,
                            8.05,
                            8.55,
                            9.05,
                            9.55,
                            10.1,
                            10.6,
                            11.2,
                            11.85,
                            12.5,
                            13.15,
                            13.75,
                            14.45,
                            15.1,
                            15.8,
                            16.55,
                            17.25,
                            17.95,
                            18.75,
                            19.55,
                            20.35,
                            21.15,
                        ],
                        '63.5' : [
                            7,
                            8,
                            9,
                            10,
                            11.1,
                            12.1,
                            13.2,
                            14.4,
                            15.5,
                            16.6,
                            17.8,
                            19.1,
                            20.3,
                            21.6,
                            22.9,
                            24.1,
                            25.7,
                            27.2,
                            28.7,
                            30.2,
                            31.8,
                            33.7,
                            35.6,
                            37.5,
                            39.4,
                            41.3,
                            43.3,
                            45.4,
                            47.4,
                            49.4,
                            51.5,
                            53.9,
                            56.3,
                            58.7,
                            61.1,
                            63.5,
                        ],
                        '65.2' : [
                            5.2,
                            6.4,
                            7.6,
                            8.7,
                            9.9,
                            11.1,
                            12.4,
                            13.7,
                            15,
                            16.3,
                            17.6,
                            19,
                            20.5,
                            21.9,
                            23.3,
                            24.8,
                            26.3,
                            27.9,
                            29.4,
                            31,
                            32.6,
                            34.5,
                            36.5,
                            38.4,
                            40.4,
                            42.3,
                            44.4,
                            46.5,
                            48.6,
                            50.7,
                            52.8,
                            55.2,
                            57.7,
                            60.2,
                            62.7,
                            65.2,
                        ],
                        '97.75' : [
                            7.8,
                            9.6,
                            11.35,
                            13.1,
                            14.85,
                            16.6,
                            18.55,
                            20.5,
                            22.5,
                            24.45,
                            26.4,
                            28.55,
                            30.7,
                            32.85,
                            35,
                            37.15,
                            39.5,
                            41.85,
                            44.15,
                            46.5,
                            48.85,
                            51.8,
                            54.75,
                            57.65,
                            60.6,
                            63.5,
                            66.65,
                            69.8,
                            72.9,
                            76.05,
                            79.15,
                            82.85,
                            86.6,
                            90.3,
                            94,
                            97.75,
                        ],
                        '104.25' : [
                            8.35,
                            10.2,
                            12.1,
                            13.95,
                            15.85,
                            17.7,
                            19.8,
                            21.9,
                            24,
                            26.05,
                            28.15,
                            30.45,
                            32.75,
                            35.05,
                            37.3,
                            39.6,
                            42.1,
                            44.6,
                            47.1,
                            49.6,
                            52.1,
                            55.25,
                            58.4,
                            61.5,
                            64.65,
                            67.75,
                            71.1,
                            74.45,
                            77.75,
                            81.1,
                            84.45,
                            88.4,
                            92.35,
                            96.3,
                            100.3,
                            104.25,
                        ],
                        '105.9' : [
                            11.6,
                            13.3,
                            15,
                            16.7,
                            18.4,
                            20.1,
                            22,
                            23.9,
                            25.8,
                            27.7,
                            29.6,
                            31.8,
                            33.9,
                            36,
                            38.1,
                            40.2,
                            42.8,
                            45.3,
                            47.9,
                            50.4,
                            52.9,
                            56.1,
                            59.3,
                            62.5,
                            65.6,
                            68.8,
                            72.2,
                            75.6,
                            79,
                            82.4,
                            85.8,
                            89.8,
                            93.8,
                            97.8,
                            101.8,
                            105.9,
                        ],
                        '130.3' : [
                            10.4,
                            12.75,
                            15.1,
                            17.45,
                            19.8,
                            22.15,
                            24.75,
                            27.35,
                            29.95,
                            32.6,
                            35.2,
                            38.05,
                            40.9,
                            43.8,
                            46.65,
                            49.5,
                            52.65,
                            55.75,
                            58.9,
                            62,
                            65.15,
                            69.05,
                            72.95,
                            76.9,
                            80.8,
                            84.7,
                            88.85,
                            93.05,
                            97.2,
                            101.35,
                            105.55,
                            110.5,
                            115.45,
                            120.4,
                            125.35,
                            130.3,
                        ],
                        '201.15' : [
                            22.15,
                            25.35,
                            28.55,
                            31.8,
                            35,
                            38.2,
                            41.85,
                            45.45,
                            49.1,
                            52.7,
                            56.3,
                            60.35,
                            64.35,
                            68.4,
                            72.4,
                            76.45,
                            81.25,
                            86.1,
                            90.9,
                            95.75,
                            100.6,
                            106.6,
                            112.65,
                            118.7,
                            124.7,
                            130.75,
                            137.2,
                            143.6,
                            150.05,
                            156.5,
                            162.95,
                            170.6,
                            178.2,
                            185.85,
                            193.5,
                            201.15,
                        ],
                        '211.75' : [
                            23.3,
                            26.7,
                            30.05,
                            33.45,
                            36.85,
                            40.25,
                            44.05,
                            48.85,
                            51.65,
                            55.5,
                            59.3,
                            63.5,
                            67.75,
                            72,
                            76.25,
                            80.45,
                            85.55,
                            90.6,
                            95.7,
                            100.8,
                            105.85,
                            112.2,
                            118.55,
                            124.95,
                            131.3,
                            137.65,
                            144.4,
                            151.2,
                            157.95,
                            164.75,
                            171.5,
                            179.55,
                            187.6,
                            195.65,
                            203.7,
                            211.75,
                        ],
                        '216' : [
                            23.75,
                            27.2,
                            30.65,
                            34.1,
                            37.6,
                            41.05,
                            44.9,
                            48.8,
                            52.7,
                            56.6,
                            60.45,
                            64.8,
                            69.1,
                            73.45,
                            77.75,
                            82.05,
                            87.25,
                            92.45,
                            97.6,
                            102.8,
                            108,
                            114.45,
                            120.95,
                            127.45,
                            133.9,
                            140.4,
                            147.3,
                            154.2,
                            161.1,
                            168.05,
                            174.95,
                            183.15,
                            191.35,
                            199.55,
                            207.75,
                            216,
                        ],
                        '222.35' : [
                            24.45,
                            28,
                            31.55,
                            35.15,
                            38.7,
                            42.25,
                            46.25,
                            50.25,
                            54.25,
                            58.25,
                            62.25,
                            66.7,
                            71.15,
                            75.6,
                            80.05,
                            84.5,
                            89.8,
                            95.15,
                            100.5,
                            105.85,
                            111.15,
                            117.85,
                            124.5,
                            131.15,
                            137.85,
                            144.5,
                            151.65,
                            158.75,
                            165.85,
                            172.95,
                            180.1,
                            188.55,
                            197,
                            205.45,
                            213.9,
                            222.35,
                        ],
                        '233.45' : [
                            25.7,
                            29.4,
                            33.15,
                            36.9,
                            40.6,
                            44.35,
                            48.55,
                            52.75,
                            56.95,
                            61.15,
                            65.35,
                            70.05,
                            74.7,
                            79.35,
                            84.05,
                            88.7,
                            94.3,
                            99.9,
                            105.5,
                            111.1,
                            116.7,
                            123.75,
                            130.75,
                            137.75,
                            144.75,
                            151.75,
                            159.2,
                            166.7,
                            174.15,
                            181.6,
                            189.1,
                            197.95,
                            206.85,
                            215.7,
                            224.55,
                            233.45,
                        ],
                        '315.05' : [
                            34.65,
                            39.7,
                            44.75,
                            49.8,
                            54.8,
                            59.85,
                            65.55,
                            71.2,
                            76.85,
                            82.55,
                            88.2,
                            94.5,
                            100.8,
                            107.1,
                            113.4,
                            119.7,
                            127.3,
                            134.85,
                            142.4,
                            149.95,
                            157.5,
                            166.95,
                            176.4,
                            185.85,
                            195.3,
                            204.75,
                            214.85,
                            224.95,
                            235,
                            245.1,
                            255.2,
                            267.15,
                            279.1,
                            291.1,
                            303.05,
                            315.05,
                        ],
                        '320.05' : [
                            33,
                            37.8,
                            42.6,
                            47.4,
                            52.2,
                            57,
                            62.4,
                            67.8,
                            73.2,
                            78.6,
                            84,
                            90,
                            96,
                            102,
                            108,
                            114,
                            121.2,
                            128.4,
                            135.6,
                            142.8,
                            150,
                            159,
                            168,
                            177,
                            186,
                            195,
                            204.6,
                            214.25,
                            223.85,
                            233.45,
                            243.05,
                            254.45,
                            265.85,
                            277.25,
                            288.65,
                            320.05,
                        ],

                    }
                },
                Formation: {
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
                    statistics: {
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
                },
                Military: {
                    General: [
                        {
                            name: 'march-slots',
                            display: 'March Slots',
                            max: 6,
                            min: 1,
                        },
                        {
                            name: 'march-capacity',
                            display: 'March Capacity',
                            min: 0,
                        },
                        {
                            name: 'training-capacity',
                            display: 'Training Capacity',
                            min: 0,
                        },
                        {
                            name: 'training-speed',
                            display: 'Training Speed',
                            min: 0,
                        },
                    ],
                    Troop: [
                        {
                            name: 'troop-attack',
                            display: 'Troop Attack',
                            min: 0,
                        },
                        {
                            name: 'troop-defense',
                            display: 'Troop Defense',
                            min: 0,
                        },
                        {
                            name: 'troop-lethality',
                            display: 'Troop Damage',
                            min: 0,
                        },
                        {
                            name: 'troop-health',
                            display: 'Troop Health',
                            min: 0,
                        },
                    ],
                    Infantry: [
                        {
                            name: 'infantry-attack',
                            display: 'Infantry Attack',
                            min: 0,
                        },
                        {
                            name: 'infantry-defense',
                            display: 'Infantry Defense',
                            min: 0,
                        },
                        {
                            name: 'infantry-lethality',
                            display: 'Infantry Lethality',
                            min: 0,
                        },
                        {
                            name: 'infantry-health',
                            display: 'Infantry Health',
                            min: 0,
                        },
                    ],
                    Hunter: [
                        {
                            name: 'hunter-attack',
                            display: 'Hunter Attack',
                            min: 0,
                        },
                        {
                            name: 'hunter-defense',
                            display: 'Hunter Defense',
                            min: 0,
                        },
                        {
                            name: 'hunter-lethality',
                            display: 'Hunter Lethality',
                            min: 0,
                        },
                        {
                            name: 'hunter-health',
                            display: 'Hunter Health',
                            min: 0,
                        },
                    ],
                    Rider: [
                        {
                            name: 'rider-attack',
                            display: 'Rider Attack',
                            min: 0,
                        },
                        {
                            name: 'rider-defense',
                            display: 'Rider Defense',
                            min: 0,
                        },
                        {
                            name: 'rider-lethality',
                            display: 'Rider Lethality',
                            min: 0,
                        },
                        {
                            name: 'rider-health',
                            display: 'Rider Health',
                            min: 0,
                        },
                    ],
                    Settlement: [
                        {
                            name: 'settlement-attack',
                            display: 'Settlement Army Attack',
                            min: 0,
                        },
                        {
                            name: 'settlement-defense',
                            display: 'Settlement Army Defense',
                            min: 0,
                        },
                        {
                            name: 'settlement-lethality',
                            display: 'Settlement Troop Lethality',
                            min: 0,
                        },
                        {
                            name: 'settlement-health',
                            display: 'Settlement Troop Health',
                            min: 0,
                        },
                    ]
                },
                HeroGear: {
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
                    slots: [
                        {
                            type: 'helmet',
                            display: 'Helmet',
                        },
                        {
                            type: 'chest',
                            display: 'Chest',
                        },
                        {
                            type: 'feet',
                            display: 'Feet',
                        }
                    ],
                    sets: {
                        brawler: [
                            {
                                tier: 1,
                                color: 'grey',
                                name: 'Strong Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 1.35,
                                            lethality: 3.05,
                                        },
                                        {
                                            health: 1.95,
                                            lethality: 5.04,
                                        },
                                        {
                                            health: 2.85,
                                            lethality: 7.55,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 3.61,
                                            lethality: 0,
                                        },
                                        {
                                            health: 6,
                                            lethality: 0,
                                        },
                                        {
                                            health: 8.92,
                                            lethality: 0,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 1.15,
                                            lethality: 3.01,
                                        },
                                        {
                                            health: 1.65,
                                            lethality: 4.56,
                                        },
                                        {
                                            health: 2.4,
                                            lethality: 6.67,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 2,
                                color: 'green',
                                name: 'Firm Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 4.1,
                                            lethality: 10.46,
                                        },
                                        {
                                            health: 5.3,
                                            lethality: 13.37,
                                        },
                                        {
                                            health: 6.5,
                                            lethality: 16.34,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 12.36,
                                            lethality: 0,
                                        },
                                        {
                                            health: 15.85,
                                            lethality: 0,
                                        },
                                        {
                                            health: 19.36,
                                            lethality: 0,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 3.4,
                                            lethality: 9.4,
                                        },
                                        {
                                            health: 4.4,
                                            lethality: 12.18,
                                        },
                                        {
                                            health: 5.4,
                                            lethality: 14.93,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 3,
                                color: 'blue',
                                name: 'Iron Wall Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 7.7,
                                            lethality: 19.36,
                                        },
                                        {
                                            health: 9.17,
                                            lethality: 22.75,
                                        },
                                        {
                                            health: 11.3,
                                            lethality: 14.05,
                                        },
                                        {
                                            health: 14.05,
                                            lethality: 30.62,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 22.87,
                                            lethality: 0,
                                        },
                                        {
                                            health: 26.87,
                                            lethality: 0,
                                        },
                                        {
                                            health: 31.65,
                                            lethality: 0,
                                        },
                                        {
                                            health: 35.83,
                                            lethality: 0,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 6.45,
                                            lethality: 17.86,
                                        },
                                        {
                                            health: 7.68,
                                            lethality: 21.2,
                                        },
                                        {
                                            health: 9.3,
                                            lethality: 25.98,
                                        },
                                        {
                                            health: 11.62,
                                            lethality: 31.38,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 4,
                                color: 'purple',
                                name: 'Fanatic Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 16.8,
                                            lethality: 34.32,
                                        },
                                        {
                                            health: 19.55,
                                            lethality: 38.02,
                                        },
                                        {
                                            health: 22.35,
                                            lethality: 41.72,
                                        },
                                        {
                                            health: 25.18,
                                            lethality: 45.5,
                                        },
                                        {
                                            health: 28.02,
                                            lethality: 49.28,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 40.02,
                                            lethality: 0,
                                        },
                                        {
                                            health: 44.2,
                                            lethality: 0,
                                        },
                                        {
                                            health: 48.45,
                                            lethality: 0,
                                        },
                                        {
                                            health: 52.71,
                                            lethality: 0,
                                        },
                                        {
                                            health: 56.96,
                                            lethality: 0,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 13.95,
                                            lethality: 36.78,
                                        },
                                        {
                                            health: 16.27,
                                            lethality: 42.18,
                                        },
                                        {
                                            health: 18.65,
                                            lethality: 47.73,
                                        },
                                        {
                                            health: 21.02,
                                            lethality: 53.41,
                                        },
                                        {
                                            health: 23.38,
                                            lethality: 59.08,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 5,
                                color: 'orange',
                                name: 'Domineering Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 30.85,
                                            lethality: 53.06,
                                        },
                                        {
                                            health: 33.69,
                                            lethality: 56.84,
                                        },
                                        {
                                            health: 36.52,
                                            lethality: 60.62,
                                        },
                                        {
                                            health: 39.36,
                                            lethality: 64.4,
                                        },
                                        {
                                            health: 43,
                                            lethality: 69.22,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 61.22,
                                            lethality: 0,
                                        },
                                        {
                                            health: 65.47,
                                            lethality: 0,
                                        },
                                        {
                                            health: 69.73,
                                            lethality: 0,
                                        },
                                        {
                                            health: 73.98,
                                            lethality: 0,
                                        },
                                        {
                                            health: 79.41,
                                            lethality: 0,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 25.75,
                                            lethality: 64.76,
                                        },
                                        {
                                            health: 28.11,
                                            lethality: 70.43,
                                        },
                                        {
                                            health: 30.48,
                                            lethality: 76.11,
                                        },
                                        {
                                            health: 32.84,
                                            lethality: 81.78,
                                        },
                                        {
                                            health: 35.84,
                                            lethality: 88.93,
                                        },
                                    ],
                                }
                            },
                        ],
                        marksman: [
                            {
                                tier: 1,
                                color: 'grey',
                                name: 'Steady Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 3.13,
                                            lethality: 0.85,
                                        },
                                        {
                                            health: 4.82,
                                            lethality: 1.25,
                                        },
                                        {
                                            health: 7.1,
                                            lethality: 1.8,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 4.11,
                                        },
                                        {
                                            health: 0,
                                            lethality: 6.7,
                                        },
                                        {
                                            health: 0,
                                            lethality: 9.97,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 2.99,
                                            lethality: 1.15,
                                        },
                                        {
                                            health: 4.78,
                                            lethality: 1.65,
                                        },
                                        {
                                            health: 7.07,
                                            lethality: 2.4,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 2,
                                color: 'green',
                                name: 'Sprint Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 10,
                                            lethality: 2.6,
                                        },
                                        {
                                            health: 12.86,
                                            lethality: 3.4,
                                        },
                                        {
                                            health: 15.74,
                                            lethality: 4.17,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 13.86,
                                        },
                                        {
                                            health: 0,
                                            lethality: 17.8,
                                        },
                                        {
                                            health: 0,
                                            lethality: 21.76,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 9.85,
                                            lethality: 3.4,
                                        },
                                        {
                                            health: 12.64,
                                            lethality: 4.4,
                                        },
                                        {
                                            health: 15.47,
                                            lethality: 5.4,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 3,
                                color: 'blue',
                                name: 'Armor Break Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 18.68,
                                            lethality: 4.96,
                                        },
                                        {
                                            health: 22.09,
                                            lethality: 5.91,
                                        },
                                        {
                                            health: 26.46,
                                            lethality: 7.19,
                                        },
                                        {
                                            health: 31.58,
                                            lethality: 8.92,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 26.07,
                                        },
                                        {
                                            health: 0,
                                            lethality: 30.68,
                                        },
                                        {
                                            health: 0,
                                            lethality: 35.75,
                                        },
                                        {
                                            health: 0,
                                            lethality: 41,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 18.34,
                                            lethality: 6.45,
                                        },
                                        {
                                            health: 21.62,
                                            lethality: 7.68,
                                        },
                                        {
                                            health: 25.69,
                                            lethality: 9.4,
                                        },
                                        {
                                            health: 29.87,
                                            lethality: 11.7,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 4,
                                color: 'purple',
                                name: 'Troop Break Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 36.7,
                                            lethality: 10.65,
                                        },
                                        {
                                            health: 41.82,
                                            lethality: 12.38,
                                        },
                                        {
                                            health: 46.96,
                                            lethality: 14.15,
                                        },
                                        {
                                            health: 52.16,
                                            lethality: 15.94,
                                        },
                                        {
                                            health: 57.36,
                                            lethality: 17.74,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 46.25,
                                        },
                                        {
                                            health: 0,
                                            lethality: 51.5,
                                        },
                                        {
                                            health: 0,
                                            lethality: 56.65,
                                        },
                                        {
                                            health: 0,
                                            lethality: 61.95,
                                        },
                                        {
                                            health: 0,
                                            lethality: 67.24,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 34.06,
                                            lethality: 14,
                                        },
                                        {
                                            health: 38.24,
                                            lethality: 16.3,
                                        },
                                        {
                                            health: 42.49,
                                            lethality: 18.65,
                                        },
                                        {
                                            health: 46.75,
                                            lethality: 21.02,
                                        },
                                        {
                                            health: 51,
                                            lethality: 23.38,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 5,
                                color: 'orange',
                                name: 'Blast Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 62.56,
                                            lethality: 19.53,
                                        },
                                        {
                                            health: 67.76,
                                            lethality: 21.33,
                                        },
                                        {
                                            health: 72.96,
                                            lethality: 23.12,
                                        },
                                        {
                                            health: 78.16,
                                            lethality: 24.92,
                                        },
                                        {
                                            health: 84.8,
                                            lethality: 27.2,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 72.54,
                                        },
                                        {
                                            health: 0,
                                            lethality: 77.83,
                                        },
                                        {
                                            health: 0,
                                            lethality: 83.13,
                                        },
                                        {
                                            health: 0,
                                            lethality: 88.42,
                                        },
                                        {
                                            health: 0,
                                            lethality: 95.07,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 55.26,
                                            lethality: 25.75,
                                        },
                                        {
                                            health: 59.51,
                                            lethality: 28.11,
                                        },
                                        {
                                            health: 63.77,
                                            lethality: 30.48,
                                        },
                                        {
                                            health: 68.02,
                                            lethality: 32.84,
                                        },
                                        {
                                            health: 73.45,
                                            lethality: 35.79,
                                        },
                                    ],
                                }
                            },
                        ],
                        scout: [
                            {
                                tier: 1,
                                color: 'grey',
                                name: 'Light Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 3.13,
                                            lethality: 1.35,
                                        },
                                        {
                                            health: 5.2,
                                            lethality: 1.95,
                                        },
                                        {
                                            health: 7.78,
                                            lethality: 2.85,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 3.81,
                                        },
                                        {
                                            health: 0,
                                            lethality: 6.35,
                                        },
                                        {
                                            health: 0,
                                            lethality: 9.42,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 2.93,
                                            lethality: 0.9,
                                        },
                                        {
                                            health: 4.41,
                                            lethality: 1.3,
                                        },
                                        {
                                            health: 6.44,
                                            lethality: 1.9,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 2,
                                color: 'green',
                                name: 'Swift Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 10.77,
                                            lethality: 4.1,
                                        },
                                        {
                                            health: 13.76,
                                            lethality: 5.3,
                                        },
                                        {
                                            health: 16.82,
                                            lethality: 6.5,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 13.06,
                                        },
                                        {
                                            health: 0,
                                            lethality: 16.7,
                                        },
                                        {
                                            health: 0,
                                            lethality: 20.41,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 9.09,
                                            lethality: 2.7,
                                        },
                                        {
                                            health: 11.78,
                                            lethality: 3.55,
                                        },
                                        {
                                            health: 14.45,
                                            lethality: 4.36,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 3,
                                color: 'blue',
                                name: 'Rapid Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 19.93,
                                            lethality: 7.7,
                                        },
                                        {
                                            health: 23.41,
                                            lethality: 9.15,
                                        },
                                        {
                                            health: 27.87,
                                            lethality: 11.3,
                                        },
                                        {
                                            health: 31.49,
                                            lethality: 14.05,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 24.17,
                                        },
                                        {
                                            health: 0,
                                            lethality: 28.41,
                                        },
                                        {
                                            health: 0,
                                            lethality: 33.55,
                                        },
                                        {
                                            health: 0,
                                            lethality: 38.21,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 17.7,
                                            lethality: 5.15,
                                        },
                                        {
                                            health: 21.02,
                                            lethality: 6.13,
                                        },
                                        {
                                            health: 24.59,
                                            lethality: 7.45,
                                        },
                                        {
                                            health: 30.21,
                                            lethality: 9.31,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 4,
                                color: 'purple',
                                name: 'Thunder Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 35.11,
                                            lethality: 16.8,
                                        },
                                        {
                                            health: 38.73,
                                            lethality: 19.55,
                                        },
                                        {
                                            health: 42.47,
                                            lethality: 22.35,
                                        },
                                        {
                                            health: 46.24,
                                            lethality: 25.18,
                                        },
                                        {
                                            health: 50.02,
                                            lethality: 28.02,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 42.87,
                                        },
                                        {
                                            health: 0,
                                            lethality: 47.52,
                                        },
                                        {
                                            health: 0,
                                            lethality: 52.15,
                                        },
                                        {
                                            health: 0,
                                            lethality: 56.87,
                                        },
                                        {
                                            health: 0,
                                            lethality: 61.6,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 35.84,
                                            lethality: 11.17,
                                        },
                                        {
                                            health: 41.47,
                                            lethality: 13.03,
                                        },
                                        {
                                            health: 46.99,
                                            lethality: 14.9,
                                        },
                                        {
                                            health: 52.66,
                                            lethality: 16.79,
                                        },
                                        {
                                            health: 58.34,
                                            lethality: 18.68,
                                        },
                                    ],
                                }
                            },
                            {
                                tier: 5,
                                color: 'orange',
                                name: 'Lightning Set',
                                steps: {
                                    helmet: [
                                        {
                                            health: 53.8,
                                            lethality: 30.85,
                                        },
                                        {
                                            health: 57.58,
                                            lethality: 33.69,
                                        },
                                        {
                                            health: 61.36,
                                            lethality: 36.52,
                                        },
                                        {
                                            health: 65.14,
                                            lethality: 39.36,
                                        },
                                        {
                                            health: 70.01,
                                            lethality: 43,
                                        },
                                    ],
                                    chest: [
                                        {
                                            health: 0,
                                            lethality: 66.32,
                                        },
                                        {
                                            health: 0,
                                            lethality: 71.05,
                                        },
                                        {
                                            health: 0,
                                            lethality: 75.77,
                                        },
                                        {
                                            health: 0,
                                            lethality: 80.5,
                                        },
                                        {
                                            health: 0,
                                            lethality: 86.57,
                                        },
                                    ],
                                    feet: [
                                        {
                                            health: 64.02,
                                            lethality: 20.57,
                                        },
                                        {
                                            health: 69.69,
                                            lethality: 22.46,
                                        },
                                        {
                                            health: 75.37,
                                            lethality: 24.35,
                                        },
                                        {
                                            health: 81.04,
                                            lethality: 26.24,
                                        },
                                        {
                                            health: 88.25,
                                            lethality: 28.67,
                                        },
                                    ],
                                }
                            },
                        ]
                    },

                }
            }
        }
    },
    methods: {
        toggleSummary()
        {
            this.ui.showSummary = !this.ui.showSummary;
        },
        selectHero(hero)
        {
            if(hero)
            {
                if(hero.type)
                {
                    this.data.Formation.heroes[hero.type] = hero.key;
                }
            }
        },
        saveLocalStorage()
        {
            localStorage.setItem('sosMilitaryData',JSON.stringify(this.data));
            console.log('Saved data to local storage');
        },
        loadLocalStorage()
        {
            let data = localStorage.getItem('sosMilitaryData');
            if(data)
            {
                this.data = JSON.parse(data);
            }
        },
        checkLocalStorage()
        {
            let data = localStorage.getItem('sosMilitaryDatasasas');
            if(data)
            {
                console.log(JSON.parse(data));
            }
        },
    },
    mounted()
    {
        this.loadLocalStorage();
    }
}
</script>

<style scoped>

</style>
