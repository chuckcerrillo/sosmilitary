<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold mb-8">Heroes</h1>
        <div class="flex items-center justify-center">


            <div>
                <div>
                    <div
                        class="rounded flex items-center justify-start text-xs p-4 font-bold"
                    >
                        <div class="w-20 pr-2">Name</div>
                        <div class="w-24">Type</div>
                        <div class="w-16">Level</div>
                        <div class="w-28">Rank</div>
                        <div class="w-12">March Capacity</div>
                        <div class="w-16 text-center">Attack</div>
                        <div class="w-16 text-center">Defense</div>
                        <div class="w-16 text-center">Lethality</div>
                        <div class="w-16 text-center">Health</div>
                    </div>
                </div>
                <div
                    v-for="(hero,num) in heroes"

                >
                    <div
                        class="rounded flex items-center justify-start text-sm h-16 px-4"
                        :class="num%2===0 ? 'bg-gray-100' : ''"
                    >
                        <div class="w-20 pr-2">{{hero.name}}</div>
                        <div class="w-24">{{types[hero.type].name}}</div>
                        <div class="w-16"><input @change="saveLocalStorage()" type="number" class="w-12 border border-gray-400 rounded p-1 text-xs" max="80" min="1"  value="1" v-model="data.Heroes[hero.key].level"></div>
                        <div class="w-28">{{ getRank(hero.key) }}</div>
                        <div class="w-12">{{getMarch(hero.key)}}</div>
                        <div class="w-16 text-center">{{getAttack(hero.key)}}%</div>
                        <div class="w-16 text-center">{{getDefense(hero.key)}}%</div>
                        <div class="w-16 text-center">{{getLethality(hero.key)}}%</div>
                        <div class="w-16 text-center">{{getHealth(hero.key)}}%</div>
                        <div class="text-xs">
                            <a @click="promote(hero.key)" class="block p-1 hover:underline text-blue-400 cursor-pointer">Promote</a>
                            <a @click="demote(hero.key)" class="block p-1 hover:underline text-blue-400 cursor-pointer">Demote</a>
                        </div>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "heroes",
    props: [
        'library',
        'data'
    ],
    data() {
        return {
        }
    },
    computed: {
        types()
        {
            return this.library.Heroes.types;
        },
        ranks()
        {
            return this.library.Heroes.ranks;
        },
        heroes()
        {
            return this.library.Heroes.heroes;
        },
        march()
        {
            return this.library.Heroes.march;
        },
        scales()
        {
            return this.library.Heroes.scales;
        }
    },
    methods: {
        getRank(key)
        {
            let hero = this.data.Heroes[key];
            let level;

            switch(hero.upgrade)
            {
                case 5:
                    level = 'V';
                    break;
                case 4:
                    level = 'IV';
                    break;
                case 3:
                    level = 'III';
                    break;
                case 2:
                    level = 'II';
                    break;
                default:
                    level = 'I';
            }
            return this.ranks[hero.rank].name + ' ' + level;
        },
        getRankValue(key)
        {
            let hero = this.data.Heroes[key];
            return hero.rank * 5 + hero.upgrade - 1;
        },
        getMarch(key)
        {
            let hero = this.data.Heroes[key];
            return this.march[hero.level - 1];
        },
        getAttack(key)
        {
            let hero = this.data.Heroes[key];
            let heroData;
            let scale;
            let x;

            if(key)
            {
                for(x in this.heroes)
                {
                    if(this.heroes[x] && this.heroes[x].key === key)
                    {
                        heroData = this.heroes[x];
                        break;
                    }
                }
            }

            if(heroData && hero)
            {
                let scale = this.scales[heroData.stats.base.attack];
                return scale[this.getRankValue(key)];
            }
            return 0;
        },
        getDefense(key)
        {
            let hero = this.data.Heroes[key];
            let heroData;
            let scale;
            let x;

            if(key)
            {
                for(x in this.heroes)
                {
                    if(this.heroes[x] && this.heroes[x].key === key)
                    {
                        heroData = this.heroes[x];
                        break;
                    }
                }
            }

            if(heroData && hero)
            {
                let scale = this.scales[heroData.stats.base.defense];
                return scale[this.getRankValue(key)];
            }
            return 0;
        },
        getLethality(key)
        {
            return 0;
        },
        getHealth(key)
        {
            return 0;
        },
        promote(key)
        {
            let hero = this.data.Heroes[key];
            if(hero.upgrade < 5)
            {
                if(hero.rank < 7)
                {
                    this.data.Heroes[key].upgrade++;
                }
            }
            else if(hero.rank < 7)
            {
                this.data.Heroes[key].rank++;
                this.data.Heroes[key].upgrade = 1;
            }
            this.$emit('saveLocalStorage');
            return true;
        },
        demote(key)
        {
            let hero = this.data.Heroes[key];
            if(hero.upgrade > 1)
            {
                this.data.Heroes[key].upgrade--;
            }
            else if(hero.rank > 1)
            {
                this.data.Heroes[key].rank--;
                this.data.Heroes[key].upgrade = 5;
            }
            this.$emit('saveLocalStorage');
            return true;
        },
        saveLocalStorage()
        {
            this.$emit('saveLocalStorage');
        },
    }
}
</script>

<style scoped>

</style>
