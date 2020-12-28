<template>
    <div class="relative">
        <h1 class="text-center text-2xl font-bold mt-8 mb-2">Summary</h1>
        <div class="flex flex-wrap items-center justify-center mb-8">

            <div class="text-center m-1 bg-gray-400 mx-2 rounded p-4 py-8 w-60">
                <div class="text-sm">
                    Total Attack Power
                </div>
                <div class="text-3xl font-bold">
                    {{ Math.round(totalAttackPower).toLocaleString() }}
                </div>
            </div>

            <div class="text-center m-1 bg-gray-400 mx-2 rounded p-4 py-8 w-60">
                <div class="text-sm">
                    Total Defense Power
                </div>
                <div class="text-3xl font-bold">
                    {{ Math.round(totalDefensePower).toLocaleString() }}
                </div>
            </div>
        </div>
        <div class="text mt-8">
            <h1 class="text-center text-2xl font-bold my-2">Power Breakdown</h1>
            <div class="flex items-start justify-center">
                <div class="lg:w-200 p-2">
                    <div class="flex items-start justify-center text-center text-sm">
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div>Attack</div>
                            <div class="font-bold text-2xl">{{ Math.round(attack).toLocaleString() }}</div>
                        </div>
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div>Defense</div>
                            <div class="font-bold text-2xl">{{ Math.round(defense).toLocaleString() }}</div>
                        </div>
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div>Lethality</div>
                            <div class="font-bold text-2xl">{{ Math.round(lethality).toLocaleString() }}</div>
                        </div>
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div>Health</div>
                            <div class="font-bold text-2xl">{{ Math.round(health).toLocaleString() }}</div>
                        </div>
                    </div>

                    <div class="flex items-start justify-center text-sm">
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Infantry</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Infantry.attack).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Hunter</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Hunter.attack).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Rider</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Rider.attack).toLocaleString() }}</div>
                            </div>
                        </div>
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Infantry</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Infantry.defense).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Hunter</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Hunter.defense).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Rider</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Rider.defense).toLocaleString() }}</div>
                            </div>
                        </div>
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Infantry</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Infantry.lethality).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Hunter</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Hunter.lethality).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Rider</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Rider.lethality).toLocaleString() }}</div>
                            </div>
                        </div>
                        <div class="w-48 m-2 p-4 rounded bg-gray-300">
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Infantry</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Infantry.health).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Hunter</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Hunter.health).toLocaleString() }}</div>
                            </div>
                            <div class="flex items-center justify-start">
                                <div class="text-left w-16">Rider</div>
                                <div class="text-right w-20 font-bold">{{ Math.round(Rider.health).toLocaleString() }}</div>
                            </div>
                        </div>
                    </div>

                    <h1 class="text-xl font-bold p-2 text-center mt-4">Boost Details</h1>
                    <div>
                        <div
                            v-for="(label,stat) in {attack:'Attack',defense:'Defense',health:'Health',lethality: 'Lethality'}"
                            class="rounded p-2 py-1 flex items-center justify-center"
                            :class="stat === 'defense' || stat === 'lethality' ? 'bg-gray-100' : ''"
                        >
                            <div class="mr-2 text-right w-40 p-1">Troop {{ label }}</div>
                            <div class="ml-2 font-bold w-40 p-1">{{ data.Military['troop-' + stat] }}%</div>
                        </div>
                        <div
                            v-for="(label,stat) in {attack:'Attack',defense:'Defense',health:'Health',lethality: 'Lethality'}"
                            class="rounded p-2 py-1 flex items-center justify-center"
                            :class="stat === 'defense' || stat === 'lethality' ? 'bg-gray-100' : ''"
                        >
                            <div class="mr-l text-right w-40 p-1">Infantry {{ label }}</div>
                            <div class="ml-2 font-bold w-40 p-1">{{getTotalBoosts()['Infantry'][stat].toFixed(2)}}%</div>
                        </div>
                        <div
                            v-for="(label,stat) in {attack:'Attack',defense:'Defense',health:'Health',lethality: 'Lethality'}"
                            class="rounded p-2 py-1 flex items-center justify-center"
                            :class="stat === 'defense' || stat === 'lethality' ? 'bg-gray-100' : ''"
                        >
                            <div class="mr-l text-right w-40 p-1">Hunter {{ label }}</div>
                            <div class="ml-2 font-bold w-40 p-1">{{getTotalBoosts()['Hunter'][stat].toFixed(2)}}%</div>
                        </div>
                        <div
                            v-for="(label,stat) in {attack:'Attack',defense:'Defense',health:'Health',lethality: 'Lethality'}"
                            class="rounded p-2 py-1 flex items-center justify-center"
                            :class="stat === 'defense' || stat === 'lethality' ? 'bg-gray-100' : ''"
                        >
                            <div class="mr-2 text-right w-40 p-1">Rider {{ label }}</div>
                            <div class="ml-2 font-bold w-40 p-1">{{getTotalBoosts()['Rider'][stat].toFixed(2)}}%</div>
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
        getTotalBoosts(pure)
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
                for(let stat of ['lethality','health'])
                {
                    for(let slot of ['helmet','chest','feet'])
                    {
                        result[types[troopType]][stat] += parseFloat(this.library.HeroGear.sets[troopType][this.data.HeroGear[troopType][slot].tier-1].steps[slot][this.data.HeroGear[troopType][slot].step-1][stat]);
                    }
                }
            }

            // Get military stats boost
            for(let statType of ['attack','defense','lethality','health'])
            {
                if (pure)
                {
                    for(let type in result)
                    {
                        result[type][statType] += parseFloat(this.data.Military['troop-' + statType]);
                    }
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
        Infantry()
        {
            let attack = 0;
            let defense = 0;
            let health = 0;
            let lethality = 0;
            let troop = 'Infantry';
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'attack',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                attack += value;
                if(this.totalBoosts[troop].attack)
                {
                    attack += value * this.totalBoosts[troop].attack/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'defense',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                defense += value;
                if(this.totalBoosts[troop].defense)
                {
                    defense += value * this.totalBoosts[troop].defense/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'lethality',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                lethality += value;
                if(this.totalBoosts[troop].lethality)
                {
                    lethality += value * this.totalBoosts[troop].lethality/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'health',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                health += value;
                if(this.totalBoosts[troop].health)
                {
                    health += value * this.totalBoosts[troop].health/100;
                }
            }

            return {
                attack: attack,
                defense: defense,
                lethality: lethality,
                health: health,
            }
        },
        Hunter()
        {
            let attack = 0;
            let defense = 0;
            let health = 0;
            let lethality = 0;
            let troop = 'Hunter';
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'attack',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                attack += value;
                if(this.totalBoosts[troop].attack)
                {
                    attack += value * this.totalBoosts[troop].attack/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'defense',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                defense += value;
                if(this.totalBoosts[troop].defense)
                {
                    defense += value * this.totalBoosts[troop].defense/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'lethality',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                lethality += value;
                if(this.totalBoosts[troop].lethality)
                {
                    lethality += value * this.totalBoosts[troop].lethality/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'health',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                health += value;
                if(this.totalBoosts[troop].health)
                {
                    health += value * this.totalBoosts[troop].health/100;
                }
            }

            return {
                attack: attack,
                defense: defense,
                lethality: lethality,
                health: health,
            }
        },
        Rider()
        {
            let attack = 0;
            let defense = 0;
            let health = 0;
            let lethality = 0;
            let troop = 'Rider';
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'attack',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                attack += value;
                if(this.totalBoosts[troop].attack)
                {
                    attack += value * this.totalBoosts[troop].attack/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'defense',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                defense += value;
                if(this.totalBoosts[troop].defense)
                {
                    defense += value * this.totalBoosts[troop].defense/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'lethality',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                lethality += value;
                if(this.totalBoosts[troop].lethality)
                {
                    lethality += value * this.totalBoosts[troop].lethality/100;
                }
            }

            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                let value = parseInt(this.getPlasma(this.formation.plasma[troop],'health',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
                health += value;
                if(this.totalBoosts[troop].health)
                {
                    health += value * this.totalBoosts[troop].health/100;
                }
            }

            return {
                attack: attack,
                defense: defense,
                lethality: lethality,
                health: health,
            }
        },
        attack()
        {
            let attack = 0;
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                for (let troop of ['Infantry','Rider','Hunter'])
                {
                    let troopAttack = parseInt(this.getPlasma(this.formation.plasma[troop],'attack',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
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
                    let troopLethality = parseInt(this.getPlasma(this.formation.plasma[troop],'lethality',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
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
                    let troopDefense = parseInt(this.getPlasma(this.formation.plasma[troop],'defense',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
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
                    let troopHealth = parseInt(this.getPlasma(this.formation.plasma[troop],'health',this.library.Formation.troops[troop][tier])) * parseInt(this.formation.quantity[troop][tier])
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
