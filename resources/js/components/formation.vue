<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold">Formation</h1>
        <div class="text-xs my-2">
            <p>This is the troop formation you'll be using in a march. Choose the appropriate heroes and troops for the activity you wish to do. For instance when attacking settlements you might want to use "Siege" heroes, etc.</p>
        </div>
        <div class="flex items-center justify-center">
            <div
                v-for="(type,index,num) in library.Formation.types"
                class="flex-col p-1 text-gray-700"
            >
                <div class="text-center">{{ type.name }}</div>
                <div
                    class="rounded w-32 h-32 border border-gray-400 bg-gray-300 items-center flex justify-center cursor-pointer"
                    :class="data.Formation.saved[data.Formation.active].captain === type.type ? 'border-blue-400':''"
                    @click="toggleHeroes(getHeroType(type.type))"
                >
                    <div v-if="data.Formation.saved[data.Formation.active].heroes[getHeroType(type.type)]">
                        {{findHero(data.Formation.saved[data.Formation.active].heroes[getHeroType(type.type)])}}
                    </div>
                    <div v-else class="text-gray-500 text-center">Choose hero...</div>
                </div>
                <div v-if="data.Formation.saved[data.Formation.active].captain === type.type"
                     class="text-sm p-2 text-center text-blue-400 font-bold">
                    Captain
                </div>
                <div v-else class="text-sm p-2 text-center text-gray-600 hover:text-blue-400 hover:underline cursor-pointer" @click="data.Formation.saved[data.Formation.active].captain = type.type">Make captain</div>

            </div>

        </div>
        <div v-show="ui.showHeroes" class="flex flex-wrap items-center justify-center">

            <div
                v-for="(hero,num) in library.Heroes.heroes"
                class="flex-col p-1 text-gray-700"
            >
                <div
                    class="rounded w-16 h-16 border items-center flex justify-center cursor-pointer"
                    :class="ui.selectedType === hero.type ? 'border-green-400 bg-green-200 text-black' : 'border-gray-400 bg-gray-200 text-gray-600'"
                    @click="selectHero(hero)"
                >
                    <div
                        class="text-center text-xs"
                    >{{ hero.name }}</div>
                </div>
            </div>

        </div>

        <h1 class="text-center text-2xl text-gray-800 font-bold my-4">Troops</h1>
        <div class="flex items-start justify-center">
            <div>
                <div class="flex items-start justify-center">
                    <div class="mr-1 p-4 border border-gray-400 rounded h-32">
                        <div>Plasma Level</div>
                        <div class="flex items-center justify-start">
                            <div
                                v-for="level in [0,1,2,3]"
                                class="p-2 m-2 text-2xl border border-gray-400 rounded w-12 h-12 text-center bg-gray-300 hover:border-blue-400 cursor-pointer"
                                :class="data.Formation.saved[data.Formation.active].plasma === level ? 'border-blue-400 text-blue-600 bg-blue-200' : ''"
                                @click="setPlasmaLevel(level)"
                            >
                                <div>{{"*".repeat(level)}}</div>
                            </div>
                        </div>
                    </div>
                    <div class="ml-1 p-4 border border-gray-400 rounded h-32">
                        <div>March Capacity</div>
                        <div class="font-bold text-3xl">{{ marchCapacity }}</div>
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
                        <div class="p-1 w-28">{{library.Formation.troops[troop][tier].name}}</div>
                        <div class="p-1 w-16">{{library.Formation.troops[troop][tier].stats.type}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.Formation.saved[data.Formation.active].plasma,'attack',library.Formation.troops[troop][tier])}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.Formation.saved[data.Formation.active].plasma,'defense',library.Formation.troops[troop][tier])}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.Formation.saved[data.Formation.active].plasma,'lethality',library.Formation.troops[troop][tier])}}</div>
                        <div class="p-1 w-16 text-right">{{getPlasma(data.Formation.saved[data.Formation.active].plasma,'health',library.Formation.troops[troop][tier])}}</div>
                        <div class="p-1 w-20"><input @change="saveLocalStorage()" type="number" class="w-20 border border-gray-400 rounded p-1 text-xs" v-model="data.Formation.quantity[troop][tier]" /></div>
                    </div>
                </div>
            </div>

        </div>
    </div>
</template>

<script>
export default {
    name: "formation",
    props: [
        'library',
        'data',
    ],
    data() {
        return {
            ui : {
                showHeroes: false,
                selectedType: '',
            }
        }
    },
    methods: {
        setPlasmaLevel(level)
        {
            this.data.Formation.saved[this.data.Formation.active].plasma = level;
            this.$emit('saveLocalStorage');
        },
        getHeroType(type)
        {
            for(let x in this.library.Heroes.types)
            {
                if(this.library.Heroes.types[x].type === type)
                {
                    return x;
                }
            }
            return type;
        },
        getTroopType(type)
        {
            return this.library.Heroes.types[type];
        },
        getPlasma(level,type,stats)
        {
            let offset = 0;
            if(level > 0)
            {
                offset = stats.plasma[level][type];
            }

            return stats.stats[type] + offset;
        },
        toggleHeroes(type)
        {
            type = this.getHeroType(type);
            if(this.ui.showHeroes && type === this.ui.selectedType)
            {
                this.ui.showHeroes = !this.ui.showHeroes;
            }
            else
            {
                this.ui.showHeroes = true;
            }
            this.ui.selectedType = type;
        },
        selectHero(hero)
        {
            this.$emit('selectHero',hero);
            this.$emit('saveLocalStorage');
        },
        findHero(key)
        {
            if(key)
            {
                for(let hero of this.library.Heroes.heroes)
                {
                    if(hero.key === key)
                    {
                        return hero.name;
                    }
                }
            }
            return false;
        },
        saveLocalStorage()
        {
            this.$emit('saveLocalStorage');
        },
    },
    computed: {
        marchCapacity()
        {
            return 0;
        }
    }
}
</script>

<style scoped>

</style>
