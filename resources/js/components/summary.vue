<template>
    <div class="text-gray-200 relative">
        <h1 class="text-center text-2xl font-bold mb-2">Summary</h1>
        <div class="flex flex-wrap items-center justify-center mb-4">

<!--            <div class="text-center m-1 mx-4">-->
<!--                <div class="text-xs">-->
<!--                    Attack-->
<!--                </div>-->
<!--                <div class="text-3xl font-bold">-->
<!--                    0.0-->
<!--                </div>-->
<!--            </div>-->

<!--            <div class="text-center m-1 mx-4">-->
<!--                <div class="text-xs">-->
<!--                    Defense-->
<!--                </div>-->
<!--                <div class="text-3xl font-bold">-->
<!--                    0.0-->
<!--                </div>-->
<!--            </div>-->

<!--            <div class="text-center m-1 mx-4">-->
<!--                <div class="text-xs">-->
<!--                    Lethality-->
<!--                </div>-->
<!--                <div class="text-3xl font-bold">-->
<!--                    0.0-->
<!--                </div>-->
<!--            </div>-->

<!--            <div class="text-center m-1 mx-4">-->
<!--                <div class="text-xs">-->
<!--                    Health-->
<!--                </div>-->
<!--                <div class="text-3xl font-bold">-->
<!--                    0.0-->
<!--                </div>-->
<!--            </div>-->

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Total Attack Power
                </div>
                <div class="text-3xl font-bold">
                    {{ totalAttackPower.toLocaleString() }}
                </div>
            </div>

            <div class="text-center m-1 mx-4">
                <div class="text-xs">
                    Total Defense Power
                </div>
                <div class="text-3xl font-bold">
                    {{ totalDefensePower.toLocaleString() }}
                </div>
            </div>
        </div>
        <div class="text-center font-bold">
            <div v-if="showSummary" class="hover:text-green-400 cursor-pointer" @click="toggleSummary()">
                Hide detailed breakdown
            </div>
            <div v-else class="hover:text-green-400 cursor-pointer" @click="toggleSummary()">
                Show detailed breakdown
            </div>
        </div>
        <div class="text-gray-200 text border-t border-gray-600 mt-4">
            <h1 class="text-center text-2xl font-bold my-2 text-white">Power Breakdown</h1>
            <div class="flex items-start justify-center">
                <div class="lg:w-200 p-2">
                    <div class="flex items-start justify-center text-center">
                        <div class="m-2 p-2">
                            <div>Attack</div>
                            <div class="font-bold text-2xl">{{ attack.toLocaleString() }}</div>
                        </div>
                        <div class="m-2 p-2">
                            <div>Defense</div>
                            <div class="font-bold text-xl">{{ defense.toLocaleString() }}</div>
                        </div>
                        <div class="m-2 p-2">
                            <div>Lethality</div>
                            <div class="font-bold text-xl">{{ lethality.toLocaleString() }}</div>
                        </div>
                        <div class="m-2 p-2">
                            <div>Health</div>
                            <div class="font-bold text-xl">{{ health.toLocaleString() }}</div>
                        </div>
                    </div>
                    <h1 class="text-xl font-bold p-2">Total Boosts</h1>
                    <div>
                        <div
                            class="p-2 py-1 flex items-center justify-center font-bold text-xs"
                        >
                            <div class="w-20 p-1">Class</div>
                            <div class="w-20 p-1">Attack</div>
                            <div class="w-20 p-1">Defense</div>
                            <div class="w-20 p-1">Lethality</div>
                            <div class="w-20 p-1">Health</div>
                        </div>
                        <div
                            v-for="(troopType,num) in ['Infantry','Hunter','Rider']"
                            class="p-2 py-1 flex items-center justify-center text-xs rounded"
                            :class="num % 2 === 0 ? 'bg-gray-600':''"
                        >
                            <div class="w-20 p-1">{{ troopType }}</div>
                            <div
                                v-for="(stat,num) in ['attack','defense','lethality','health']"
                                class="w-20 p-1"

                            >

                                {{getTotalBoosts()[troopType][stat].toFixed(2)}}%
                            </div>
                        </div>
                    </div>

                    <h1 class="text-xl font-bold p-2">Hero Boosts</h1>
                    <div>
                        <div
                            class="p-2 py-1 flex items-center justify-center font-bold text-xs"
                        >
                            <div class="w-20 p-1">Class</div>
                            <div class="w-20 p-1">Attack</div>
                            <div class="w-20 p-1">Defense</div>
                            <div class="w-20 p-1">Lethality</div>
                            <div class="w-20 p-1">Health</div>
                        </div>
                        <div
                            v-for="(troopType,num) in ['Infantry','Hunter','Rider']"
                            class="p-2 py-1 flex items-center justify-center text-xs rounded"
                            :class="num % 2 === 0 ? 'bg-gray-600':''"
                        >
                            <div class="w-20 p-1">{{ troopType }}</div>
                            <div
                                v-for="(stat,num) in ['attack','defense','lethality','health']"
                                class="w-20 p-1"

                            >

                                {{getTotalBoosts()[troopType][stat].toFixed(2)}}%
                            </div>
                        </div>
                    </div>

<!--                    <h1 class="text-xl font-bold p-2">Troop Power</h1>-->
<!--                    <div>-->
<!--                        <div-->
<!--                            class="p-2 py-1 flex items-center justify-center font-bold text-xs"-->
<!--                        >-->
<!--                            <div class="w-20 p-1">Class</div>-->
<!--                            <div class="w-20 p-1">Attack</div>-->
<!--                            <div class="w-20 p-1">Defense</div>-->
<!--                            <div class="w-20 p-1">Lethality</div>-->
<!--                            <div class="w-20 p-1">Health</div>-->
<!--                        </div>-->
<!--                        <div-->
<!--                            v-for="(troopType,num) in ['Infantry','Hunter','Rider']"-->
<!--                            class="p-2 py-1 flex items-center justify-center text-xs rounded"-->
<!--                            :class="num % 2 === 0 ? 'bg-gray-600':''"-->
<!--                        >-->
<!--                            <div class="w-20 p-1">{{ troopType }}</div>-->
<!--                            <div-->
<!--                                v-for="(stat,num) in ['attack','defense','lethality','health']"-->
<!--                                class="w-20 p-1"-->

<!--                            >-->

<!--                                {{getTotalBoosts()[troopType][stat].toFixed(2)}}%-->
<!--                            </div>-->
<!--                        </div>-->
<!--                    </div>-->
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "summary",
    props: [
        'showSummary',
        'library',
        'data',
    ],
    data() {
        return {
        }
    },
    methods: {
        toggleSummary()
        {
            this.$emit('toggleSummary');
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
        getHero(key)
        {
            if(key)
            {
                for(let hero of this.library.Heroes.heroes)
                {
                    if(hero.key === key)
                    {
                        return hero;
                    }
                }
            }
            return false;
        },
        getRankValue(key)
        {
            let hero = this.data.Heroes[key];
            return hero.rank * 5 + hero.upgrade - 1;
        },
        getHeroStats(key)
        {
            let result = {
                attack: 0,
                defense: 0,
                lethality: 0,
                health: 0,
            }
            if(key)
            {
                if (this.data.Heroes[key])
                {
                    let hero = false;
                    for(let x in this.library.Heroes.heroes)
                    {
                        if(this.library.Heroes.heroes[x].key === key)
                        {
                            hero = this.library.Heroes.heroes[x];
                        }
                    }
                    if(hero)
                    {
                        let heroBase = hero.stats.base;
                        result.attack = this.library.Heroes.scales[heroBase.attack][this.getRankValue(key)];
                        result.defense = this.library.Heroes.scales[heroBase.defense][this.getRankValue(key)];
                    }
                }
            }
            return result;
        },
        getTotalBoosts()
        {
            let result = {
                Infantry: {
                    attack: 0,
                    defense: 0,
                    lethality: 0,
                    health: 0,
                },
                Hunter: {
                    attack: 0,
                    defense: 0,
                    lethality: 0,
                    health: 0,
                },
                Rider: {
                    attack: 0,
                    defense: 0,
                    lethality: 0,
                    health: 0,
                },
            };

            // Get hero boosts
            let formationHeroes = this.formation.heroes;
            for(let troopType in formationHeroes)
            {
                let hero = false;
                if(this.getHeroType(troopType) === 'brawler')
                {
                    result.Infantry = this.getHeroStats(formationHeroes[troopType]);
                }
                else if(this.getHeroType(troopType) === 'marksman')
                {
                    result.Hunter = this.getHeroStats(formationHeroes[troopType]);
                }
                else if(this.getHeroType(troopType) === 'scout')
                {
                    result.Rider = this.getHeroStats(formationHeroes[troopType]);
                }
            }

            // Get hero gear boosts
            let types = {brawler:'Infantry',marksman:'Hunter',scout:'Rider'}
            for(let troopType in types)
            {
                result[types[troopType]].lethality += this.library.HeroGear.sets[troopType][this.data.HeroGear.brawler.helmet.tier-1].steps.helmet[this.data.HeroGear.brawler.helmet.step-1].lethality;
                result[types[troopType]].lethality += this.library.HeroGear.sets[troopType][this.data.HeroGear.brawler.chest.tier-1].steps.helmet[this.data.HeroGear.brawler.chest.step-1].lethality;
                result[types[troopType]].lethality += this.library.HeroGear.sets[troopType][this.data.HeroGear.brawler.feet.tier-1].steps.helmet[this.data.HeroGear.brawler.feet.step-1].lethality;

                result[types[troopType]].health += this.library.HeroGear.sets[troopType][this.data.HeroGear.brawler.helmet.tier-1].steps.helmet[this.data.HeroGear.brawler.helmet.step-1].health;
                result[types[troopType]].health += this.library.HeroGear.sets[troopType][this.data.HeroGear.brawler.chest.tier-1].steps.helmet[this.data.HeroGear.brawler.chest.step-1].health;
                result[types[troopType]].health += this.library.HeroGear.sets[troopType][this.data.HeroGear.brawler.feet.tier-1].steps.helmet[this.data.HeroGear.brawler.feet.step-1].health;
            }

            // Get military stats boost
            for(let statType of ['attack','defense','lethality','health'])
            {
                for(let type in result)
                {
                    result[type][statType] += parseFloat(this.data.Military['troop-' + statType]);
                }

                result.Infantry[statType] += parseFloat(this.data.Military['infantry-' + statType]);
                result.Hunter[statType] += parseFloat(this.data.Military['hunter-' + statType]);
                result.Rider[statType] += parseFloat(this.data.Military['rider-' + statType]);


            }

            return result;
        },

        getAttack(key)
        {
            if(key && key.length > 0)
            {
                let hero = this.library.Heroes.heroes[key];
                let heroData;
                let scale;
                let x;

                if(heroData && hero)
                {
                    scale = this.library.Heroes.scales[heroData.stats.base.attack];
                    return scale[this.getRankValue(key)];
                }
            }
            return 0;
        },
        getDefense(key)
        {
            if(key && key.length > 0)
            {
                let hero = this.library.Heroes.heroes[key];
                let heroData;
                let scale;
                let x;

                if(heroData && hero)
                {
                    scale = this.library.Heroes.scales[heroData.stats.base.defense];
                    return scale[this.getRankValue(key)];
                }
            }
            return 0;
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
    },
    computed: {
        formation()
        {
            if(this.data.Formation)
            {
                if(this.data.Formation.active && this.data.Formation.saved && this.data.Formation.saved[this.data.Formation.active])
                {
                    return this.data.Formation.saved[this.data.Formation.active];
                }
            }
            return this.data.Formation.saved[0];
        },
        attack()
        {
            let attack = 0;
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                for (let troop of ['Infantry','Rider','Hunter'])
                {
                    let troopAttack = parseInt(this.getPlasma(this.formation.plasma,'attack',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                    attack += troopAttack;
                    if(this.totalBoosts[troop].attack)
                    {
                        attack += troopAttack * this.totalBoosts[troop].attack/100;
                    }
                }
            }
            return attack;
        },
        lethality()
        {
            let lethality = 0;
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                for (let troop of ['Infantry','Rider','Hunter'])
                {
                    let troopLethality = parseInt(this.getPlasma(this.formation.plasma,'lethality',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                    lethality += troopLethality;
                    if(this.totalBoosts[troop].lethality)
                    {
                        lethality += troopLethality * this.totalBoosts[troop].lethality/100;
                    }
                }
            }
            return lethality;
        },
        defense()
        {
            let defense = 0;
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                for (let troop of ['Infantry','Rider','Hunter'])
                {
                    let troopDefense = parseInt(this.getPlasma(this.formation.plasma,'defense',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                    defense += troopDefense;
                    if(this.totalBoosts[troop].defense)
                    {
                        defense += troopDefense * this.totalBoosts[troop].defense/100;
                    }
                }
            }
            return defense;
        },
        health()
        {
            let health = 0;
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                for (let troop of ['Infantry','Rider','Hunter'])
                {
                    let troopHealth = parseInt(this.getPlasma(this.formation.plasma,'health',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                    health += troopHealth;
                    if(this.totalBoosts[troop].health)
                    {
                        health += troopHealth * this.totalBoosts[troop].health/100;
                    }
                }
            }
            return health;
        },
        totalBoosts()
        {
            return this.getTotalBoosts();
        },
        totalAttackPower()
        {
            return this.attack + this.lethality;
        },
        totalDefensePower()
        {
            return this.defense + this.health;
        },
        selectedHeroes()
        {
            return this.formation.heroes;
        },
        isReady()
        {
            if(this.data && this.formation && this.formation.heroes && this.formation.heroes.brawler)
            {
                return true;
            }
            return false;
        }
    }
}
</script>

<style scoped>

</style>
