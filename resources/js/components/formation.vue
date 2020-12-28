<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold">Formation</h1>
        <div class="text-xs my-2">
            <p>This is the troop formation you'll be using in a march. Choose the appropriate heroes and troops for the activity you wish to do. For instance when attacking settlements you might want to use "Siege" heroes, etc.</p>
        </div>
        <div class="text-center">
            <h2>Saved formation slots</h2>
        </div>
        <div class="flex items-center justify-center">
            <div
                v-for="slot in [0,1,2,3,4]"
                class="p-2 rounded m-1 border border-gray-400 cursor-pointer"
                :class="data.Formation.active === slot ? 'border-blue-600 text-white bg-blue-600' : 'text-gray-800'"
                @click="data.Formation.active = slot"
            >
                Slot {{slot+1}}
            </div>
        </div>
        <div class="flex items-center justify-center">
            <div
                v-for="(type,index,num) in library.Formation.types"
                class="flex-col p-1 text-gray-700"
            >
                <div class="text-center">{{ type.name }}</div>
                <div
                    class="rounded w-32 h-36 border border-gray-400 bg-gray-300 items-center flex justify-center cursor-pointer"
                    :class="formation.captain === type.type ? 'border-blue-400':''"
                    @click="toggleHeroes(getHeroType(type.type))"
                >
                    <div v-if="formation.heroes[getHeroType(type.type)]">
                        <div class="text-center font-bold text-xs">{{findHero(formation.heroes[getHeroType(type.type)])}}</div>
                        <div><img class="w-full" :src="'img/heroes/' + findHero(formation.heroes[getHeroType(type.type)]).toLowerCase() + '.png'"></div>
                    </div>
                    <div v-else class="text-gray-500 text-center">Choose hero...</div>
                </div>
                <div v-if="formation.captain === type.type"
                     class="text-sm p-2 text-center text-blue-400 font-bold">
                    Captain
                </div>
                <div v-else class="text-sm p-2 text-center text-gray-600 hover:text-blue-400 hover:underline cursor-pointer" @click="formationcaptain = type.type">Make captain</div>

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
        <div class="flex items-start justify-center p-2">
            <div>
                <div class="flex items-start justify-center">
                    <div class="p-4 border border-gray-400 rounded">
                        <div>Plasma Level</div>
                        <div>
                            <div v-for="troopType in ['Infantry','Rider','Hunter']" class="flex items-center justify-start">
                                <div class="text-sm lg:text-base w-16 lg:w-20">{{troopType}}</div>
                                <div
                                    v-for="level in [0,1,2,3,4,5]"
                                    class="p-1 lg:p-2 m-1 lg:m-2 text-base lg:text-2xl border border-gray-400 rounded w-12 lg:w-20 lg:h-12 text-center bg-gray-300 hover:border-blue-400 cursor-pointer"
                                    :class="formation.plasma[troopType] === level ? 'border-blue-400 text-blue-600 bg-blue-200' : ''"
                                    @click="setPlasmaLevel(troopType,level)"
                                >
                                    <div class="hidden lg:block">{{"*".repeat(level)}}</div>
                                    <div class="lg:hidden">{{level}}</div>
                                </div>
                            </div>
                        </div>
                    </div>
                </div>
                <div class="mt-1 p-4 border border-gray-400 rounded h-32">
                    <div>March Capacity</div>
                    <div class="font-bold text-3xl">
                        <span :class="capacity>marchCapacity ? 'text-red-600':''">{{capacity}}</span>
                        /
                        <span>{{ marchCapacity }}</span>
                    </div>
                </div>
                <div class="mt-4 p-2">
                    <div class="flex p-1 text-xs">
                        <div class="p-1 w-16 lg:w-24"></div>
<!--                        <div class="p-1 w-8"></div>-->
                        <div class="hidden lg:block p-1 w-28">Troop</div>
                        <div class="lg:hidden p-1 w-24">Troop</div>
<!--                        <div class="p-1 w-16">Type</div>-->
                        <div class="hidden lg:block p-1 w-16 text-right">Attack</div>
                        <div class="hidden lg:block p-1 w-16 text-right">Defense</div>
                        <div class="hidden lg:block p-1 w-16 text-right">Lethality</div>
                        <div class="hidden lg:block p-1 w-16 text-right">Health</div>

                        <div class="lg:hidden p-1 w-8 text-right">A</div>
                        <div class="lg:hidden p-1 w-8 text-right">D</div>
                        <div class="lg:hidden p-1 w-8 text-right">L</div>
                        <div class="lg:hidden p-1 w-8 text-right">H</div>

                        <div class="block p-1 ml-4 w-20">Quantity</div>
                    </div>
                </div>

                <div
                    v-for="tier in [9,8,7,6,5,4,3,2,1,0]"
                    class="p-2"
                >
                    <div
                        v-for="(troop,index) in ['Infantry','Rider','Hunter']"
                        class="flex p-1 text-sm items-center"
                    >
                        <div class="p-1 w-16 lg:w-24 text-right"><img class="w-full" :src="'img/troops/t' + (tier+1) + troop.substr(0,1).toLowerCase() + '.jpg'"></div>
<!--                        <div class="p-1 w-8 text-right">T{{tier+1}}</div>-->
                        <div class="hidden lg:block p-1 w-28">
                            <div class="text-base font-bold">{{library.Formation.troops[troop][tier].name}}</div>
                            <div>{{troop}}</div>
                        </div>

                        <div class="lg:hidden p-1 w-24">
                            <div class="text-sm font-bold">{{library.Formation.troops[troop][tier].name}}</div>
                            <div class="text-xs">{{troop}}</div>
                        </div>

<!--                        <div class="p-1 w-16">{{library.Formation.troops[troop][tier].stats.type}}</div>-->
                        <div class="hidden lg:block text-xl p-1 w-16 text-right">{{getPlasma(formation.plasma[troop],'attack',library.Formation.troops[troop][tier])}}</div>
                        <div class="hidden lg:block text-xl p-1 w-16 text-right">{{getPlasma(formation.plasma[troop],'defense',library.Formation.troops[troop][tier])}}</div>
                        <div class="hidden lg:block text-xl p-1 w-16 text-right">{{getPlasma(formation.plasma[troop],'lethality',library.Formation.troops[troop][tier])}}</div>
                        <div class="hidden lg:block text-xl p-1 w-16 text-right">{{getPlasma(formation.plasma[troop],'health',library.Formation.troops[troop][tier])}}</div>

                        <div class="lg:hidden text-sm p-1 w-8 text-right">{{getPlasma(formation.plasma[troop],'attack',library.Formation.troops[troop][tier])}}</div>
                        <div class="lg:hidden text-sm p-1 w-8 text-right">{{getPlasma(formation.plasma[troop],'defense',library.Formation.troops[troop][tier])}}</div>
                        <div class="lg:hidden text-sm p-1 w-8 text-right">{{getPlasma(formation.plasma[troop],'lethality',library.Formation.troops[troop][tier])}}</div>
                        <div class="lg:hidden text-sm p-1 w-8 text-right">{{getPlasma(formation.plasma[troop],'health',library.Formation.troops[troop][tier])}}</div>

                        <div class="p-1 ml-4 w-20"><input @change="saveLocalStorage()" type="number" class="w-20 border border-gray-400 rounded p-1 text-xs" v-model="formation.quantity[troop][tier]" /></div>
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
            },
            settings: {
                totalSlots: 5
            }
        }
    },
    mounted() {

    },
    methods: {
        setPlasmaLevel(troopType,level)
        {
            this.formation.plasma[troopType] = level;
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
        getMarch(key)
        {
            if(key){
                let hero = this.data.Heroes[key];
                return this.library.Heroes.march[hero.level - 1];
            }
            return 0;
        },
        saveLocalStorage()
        {
            this.$emit('saveLocalStorage');
        },
    },
    computed: {
        marchCapacity()
        {
            let capacity = 0;
            capacity += parseInt(this.data.Military['march-capacity']);

            for(let x in this.formation.heroes)
            {
                capacity += this.getMarch(this.formation.heroes[x]);
            }

            return capacity;
        },
        capacity()
        {
            let total = 0;
            let troop = '';
            for(let troop of ['Infantry','Rider','Hunter'])
            {
                for(let tier of [0,1,2,3,4,5,6,7,8,9])
                {
                    if(this.formation && this.formation.quantity && this.formation.quantity[troop] && this.formation.quantity[troop][tier])
                    {
                        total += parseInt(this.formation.quantity[troop][tier]);
                    }
                }
            }
            return total;
        },
        formation()
        {
            return this.data.Formation.saved[this.data.Formation.active];
        },
    }
}
</script>

<style scoped>

</style>
