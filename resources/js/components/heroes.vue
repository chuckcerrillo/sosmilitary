<template>
    <div>
        <h1 class="text-center text-2xl text-gray-800 font-bold mb-8">Heroes</h1>
        <div class="flex items-center justify-center">


            <div>
                <div>
                    <div
                        class="rounded flex items-center justify-start text-xs text-center"
                    >
                        <div class="w-32">Name</div>
                        <div class="w-24">Type</div>
                        <div class="pr-2">Rank</div>
                        <div class="w-16 text-right">Attack</div>
                        <div class="w-16 text-right">Defense</div>
                        <div class="w-16 text-right">Lethality</div>
                        <div class="w-16 text-right">Health</div>
                    </div>
                </div>
                <div
                    v-for="(hero,index,num) in heroes"

                >
                    <div
                        class="rounded flex items-center justify-start text-sm"
                    >
                        <div class="w-32">{{hero.name}}</div>
                        <div class="w-24">{{types[hero.type].name}}</div>
                        <div class="pr-2">[rank]</div>
                        <div class="w-16 text-right">0.0%</div>
                        <div class="w-16 text-right">0.0%</div>
                        <div class="w-16 text-right">0.0%</div>
                        <div class="w-16 text-right">0.0%</div>
                    </div>

                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "heroes",
    data() {
        return {
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
            heroes: [
                {
                    name: 'Rusty',
                    type: 'brawler'
                },
                {
                    name: 'Ghost',
                    type: 'scout'
                },
                {
                    name: 'Sarge',
                    type: 'marksman'
                },
                {
                    name: 'Travis',
                    type: 'scout'
                },
                {
                    name: 'Mike',
                    type: 'marksman'
                },
                {
                    name: 'Eva',
                    type: 'marksman'
                },
                {
                    name: 'Tony',
                    type: 'scout'
                },
                {
                    name: 'Basel',
                    type: 'scout'
                },
                {
                    name: 'Candy',
                    type: 'scout'
                },
                {
                    name: 'Jane',
                    type: 'scout'
                },
                {
                    name: 'Chef',
                    type: 'brawler'
                },
                {
                    name: 'Maddie and Frank',
                    type: 'scout'
                },
                {
                    name: 'Nikola',
                    type: 'brawler'
                },
                {
                    name: 'Lucky',
                    type: 'marksman'
                },
                {
                    name: 'Ray and Rolex',
                    type: 'brawler'
                },
                {
                    name: 'Wolfe',
                    type: 'brawler'
                },
                {
                    name: 'Trish',
                    type: 'scout'
                },
                {
                    name: 'Jeb',
                    type: 'marksman'
                },
                {
                    name: 'Ash',
                    type: 'brawler'
                },
                {
                    name: 'Zoe',
                    type: 'marksman'
                },
                {
                    name: 'Miho',
                    type: 'scout'
                },
            ]
        }
    }
}
</script>

<style scoped>

</style>
