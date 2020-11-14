<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center text-2xl text-gray-800 font-bold">Military Stats</h1>
        <div class="text-xs my-2">
            <p>These are the stats that you will find in your stats screen. You can get there by opening your chief and choosing "stats" from the bottom menu. Once in the chief profile, scroll down to the "Military" section.</p>
        </div>

        <div class="flex flex-wrap items-center justify-center">

            <div
                v-for="(types,index,num) in library.Military"
                class="flex-col p-1 text-gray-700"
            >
                <div class="tracking-tight text-center text-xl">{{ index }} Bonuses</div>
                <div
                    v-for="stat in types"
                    class="flex p-1 text-xs items-center"
                >
                    <div class="w-48">{{stat.display}}</div>
                    <div v-if="index == 'General'"><input @change="saveLocalStorage()" class="p-1 border border-gray-400 rounded w-16 text-sm" type="number" :max="stat.max !== false ?stat.max:'false'" :min="stat.min !== false ?stat.min:'false'" v-model="data.Military[stat.name]" /></div>
                    <div v-else><input @change="saveLocalStorage()" class="p-1 border border-gray-400 rounded w-16 text-sm mr-1" type="number" :max="stat.max !== false ?stat.max:'false'" :min="stat.min !== false ?stat.min:'false'" v-model="data.Military[stat.name]" />%</div>
                </div>

            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "military-stats",
    props: [
        'library',
        'data'
    ],
    data() {
        return {
        }
    },
    methods: {
        saveLocalStorage()
        {
            this.$emit('saveLocalStorage');
        }
    }
}
</script>

<style scoped>

</style>
