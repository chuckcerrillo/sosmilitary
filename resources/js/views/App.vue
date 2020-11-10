<template>
    <div class="flex-col flex-1 h-screen overflow-y-hidden bg-gray-200 relative">
        <div class="w-full bg-gray-800 text-white h-32">
            <div class="text-2xl font-bold p-4 tracking-tighter">State of Survival - Military Calculator</div>
            <div class="flex items-center justify-center">
                <div class="p-4 px-8">My Stats</div>
                <div class="p-4 px-8">Solo Attack</div>
                <div class="p-4 px-8">Rally vs Enemy Settlement</div>
                <div class="p-4 px-8">Rally vs Influencer Trap</div>
            </div>
        </div>
        <div class="overflow-y-auto fixed inset-x-0 h-auto" style="top:8rem; bottom: 16rem;">
            <MilitaryStats :library="library" :data="data" class="border-b border-gray-400 py-8" />
            <Formation
                v-on:selectHero="selectHero"
                :library="library"
                :data="data"
                class="border-b border-gray-400 py-8"
            />
            <Heroes :library="library" :data="data" class="border-b border-gray-400 py-8" />
            <HeroGear :library="library" :data="data" class="border-b border-gray-400 py-8" />
        </div>
        <div class="fixed z-10 bottom-0 inset-x-0 bg-gray-800 text-white mb-24" :class="ui.showSummary ? 'h-128' : 'h-40'">
            <Summary
                v-on:toggleSummary="toggleSummary"
                :library="library"
                :data="data"
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
            data: {
                Formation: {
                    captain: 'infantry',
                    heroes: {
                        brawler: '',
                        marksman: '',
                        scout: '',
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
                },

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
    },
    methods: {
        toggleSummary() {
            this.ui.showSummary = !this.ui.showSummary;
        },
        selectHero(hero)
        {
            console.log('Selecting hero...');
            console.log(hero);
            if(hero)
            {
                if(hero.type)
                {
                    this.data.Formation.heroes[hero.type] = hero.key;
                }
            }
        }
    }
}
</script>

<style scoped>

</style>
