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
                    {{ totalAttackPower.toLocaleString() }}
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
        getPlasma(level,type,stats){
            let offset = 0;
            if(level > 0)
            {

                offset = stats.plasma[level][type];
            }
            return stats.stats[type] + offset;
        },
    },
    computed: {
        attack()
        {
            let attack = 0;
            for(let tier in [9,8,7,6,5,4,3,2,1,0])
            {
                for (let troop of ['Infantry','Rider','Hunter'])
                {
                    attack += parseInt(this.getPlasma(this.data.Formation.plasma,'attack',this.library.Formation.troops[troop][tier])) * parseInt(this.data.Formation.quantity[troop][tier]);
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
                    lethality += parseInt(this.getPlasma(this.data.Formation.plasma,'lethality',this.library.Formation.troops[troop][tier])) * parseInt(this.data.Formation.quantity[troop][tier]);
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
                    defense += parseInt(this.getPlasma(this.data.Formation.plasma,'defense',this.library.Formation.troops[troop][tier])) * parseInt(this.data.Formation.quantity[troop][tier]);
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
                    health += parseInt(this.getPlasma(this.data.Formation.plasma,'health',this.library.Formation.troops[troop][tier])) * parseInt(this.data.Formation.quantity[troop][tier]);
                }
            }
            return health;
        },
        totalAttackPower()
        {
            return this.attack + this.lethality;
        },
        totalDefensePower()
        {
            return this.defense + this.health;
        }
    }
}
</script>

<style scoped>

</style>
