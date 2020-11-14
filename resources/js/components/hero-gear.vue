<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold mb-8">Hero Gear</h1>
        <div class="m-auto w-180">
            <div
                v-for="(type,index,num) in library.HeroGear.types"
                class="flex p-1 text-gray-700 border items-center justify-center"
            >
                <div class="w-24">{{ type.name }}</div>

                <div
                    v-for="slot in library.HeroGear.slots"
                >
                    <div class="text-center mx-1 px-1 text-xs">{{ slot.display }}</div>
                    <div class="flex">
                        <div
                            class="rounded w-36 border border-gray-400 bg-gray-300 items-center justify-center m-1 p-2"
                            :class="'bg-' + gears[index][slot.type].color + '-200'"
                        >
                            <div class="text-center text-sm">{{gears[index][slot.type].name}}</div>
                            <div class="text-yellow-600 font-bold text-center text-3xl">
                                {{"*".repeat(gears[index][slot.type].step)}}
                            </div>
                            <div class="text-xs text-center">
                                <button @change="saveLocalStorage()" @click="upgrade(index,slot.type)" class="p-1 m-1 text-xs rounded hover:bg-green-400 hover:text-white cursor-pointer">Upgrade</button>
                                <button @change="saveLocalStorage()" @click="downgrade(index,slot.type)" class="p-1 m-1 text-xs rounded hover:bg-red-400 hover:text-white cursor-pointer">Downgrade</button>
                            </div>
                        </div>
                    </div>
                </div>
                <div>
                    <div class="w-32 text-xs p-1 font-bold">Total Boosts:</div>
                    <div class="flex w-32 text-xs">
                        <div class="w-16 p-1">Lethality</div>
                        <div class="p-1">{{ (gears[index].helmet.stats.lethality + gears[index].chest.stats.lethality + gears[index].feet.stats.lethality).toFixed(2) }}%</div>
                    </div>
                    <div class="flex w-32 text-xs">
                        <div class="w-16 p-1">Health</div>
                        <div class="p-1">{{ (gears[index].helmet.stats.health + gears[index].chest.stats.health + gears[index].feet.stats.health).toFixed(2) }}%</div>
                    </div>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "hero-gear",
    props: [
        'data',
        'library',
    ],
    data() {
        return {

        }
    },
    computed: {
        gears()
        {
            return {
                brawler: this.brawler,
                marksman: this.marksman,
                scout: this.scout,
            }
        },
        brawler()
        {
            let data = {
                helmet: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                },
                chest: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                },
                feet: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                }
            }

            data = Object.assign(data,this.data.HeroGear.brawler);

            data.helmet.name = this.library.HeroGear.sets.brawler[data.helmet.tier-1].name;
            data.helmet.color = this.library.HeroGear.sets.brawler[data.helmet.tier-1].color;
            console.log(this.library.HeroGear.sets.brawler[data.helmet.tier-1])
            data.helmet.stats = this.library.HeroGear.sets.brawler[data.helmet.tier-1].steps.helmet[data.helmet.step-1];

            data.chest.name = this.library.HeroGear.sets.brawler[data.chest.tier-1].name;
            data.chest.color = this.library.HeroGear.sets.brawler[data.chest.tier-1].color;
            data.chest.stats = this.library.HeroGear.sets.brawler[data.chest.tier-1].steps.chest[data.chest.step-1];

            data.feet.name = this.library.HeroGear.sets.brawler[data.feet.tier-1].name;
            data.feet.color = this.library.HeroGear.sets.brawler[data.feet.tier-1].color;
            data.feet.stats = this.library.HeroGear.sets.brawler[data.feet.tier-1].steps.feet[data.feet.step-1];


            return data;
        },
        marksman()
        {
            let data = {
                helmet: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                },
                chest: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                },
                feet: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                }
            }

            data = Object.assign(data,this.data.HeroGear.marksman);

            data.helmet.name = this.library.HeroGear.sets.marksman[data.helmet.tier-1].name;
            data.helmet.color = this.library.HeroGear.sets.marksman[data.helmet.tier-1].color;
            data.helmet.stats = this.library.HeroGear.sets.marksman[data.helmet.tier-1].steps.helmet[data.helmet.step-1];
            data.chest.name = this.library.HeroGear.sets.marksman[data.chest.tier-1].name;
            data.chest.color = this.library.HeroGear.sets.marksman[data.chest.tier-1].color;
            data.chest.stats = this.library.HeroGear.sets.marksman[data.chest.tier-1].steps.chest[data.chest.step-1];
            data.feet.name = this.library.HeroGear.sets.marksman[data.feet.tier-1].name;
            data.feet.color = this.library.HeroGear.sets.marksman[data.feet.tier-1].color;
            data.feet.stats = this.library.HeroGear.sets.marksman[data.feet.tier-1].steps.feet[data.feet.step-1];

            return data;
        },
        scout()
        {
            let data = {
                helmet: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                },
                chest: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                },
                feet: {
                    tier: 1,
                    step: 1,
                    stats: {
                    }
                }
            }

            data = Object.assign(data,this.data.HeroGear.scout);

            data.helmet.name = this.library.HeroGear.sets.scout[data.helmet.tier-1].name;
            data.helmet.color = this.library.HeroGear.sets.scout[data.helmet.tier-1].color;
            data.helmet.stats = this.library.HeroGear.sets.scout[data.helmet.tier-1].steps.helmet[data.helmet.step-1];
            data.chest.name = this.library.HeroGear.sets.scout[data.chest.tier-1].name;
            data.chest.color = this.library.HeroGear.sets.scout[data.chest.tier-1].color;
            data.chest.stats = this.library.HeroGear.sets.scout[data.chest.tier-1].steps.chest[data.chest.step-1];
            data.feet.name = this.library.HeroGear.sets.scout[data.feet.tier-1].name;
            data.feet.color = this.library.HeroGear.sets.scout[data.feet.tier-1].color;
            data.feet.stats = this.library.HeroGear.sets.scout[data.feet.tier-1].steps.feet[data.feet.step-1];

            return data;
        }
    },
    methods: {
        upgrade(heroType,slot)
        {
            if(this.data.HeroGear[heroType][slot])
            {
                let item = this.data.HeroGear[heroType][slot];
                if(item.tier <= this.library.HeroGear.sets[heroType].length)
                {
                    if (item.tier < this.library.HeroGear.sets[heroType].length) // item is not highest tier
                    {
                        if(item.step < this.library.HeroGear.sets[heroType][item.tier-1].steps[slot].length)
                        {
                            item.step++;
                        }
                        else
                        {
                            item.step = 1;
                            item.tier++;
                        }
                    }
                    else if (item.tier === 5 && item.step < this.library.HeroGear.sets[heroType][item.tier-1].steps[slot].length) // item is not maxed
                    {
                        if(item.step < this.library.HeroGear.sets[heroType][item.tier-1].steps[slot].length)
                        {
                            item.step++;
                        }
                    }
                }
            }
        },
        downgrade(heroType,slot)
        {
            if(this.data.HeroGear[heroType][slot])
            {
                let item = this.data.HeroGear[heroType][slot];
                if(item.tier >= 1)
                {
                    if (item.tier > 1) // item is not lowest tier
                    {
                        if(item.step > 1)
                        {
                            item.step--;
                        }
                        else
                        {
                            item.step = this.library.HeroGear.sets[heroType][item.tier-2].steps[slot].length;
                            item.tier--;
                        }
                    }
                    else if (item.tier === 1 && item.step > 1) // item is not lowest step
                    {
                        item.step--;
                    }
                }
            }
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
