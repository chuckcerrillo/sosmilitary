<template>
    <div class="lg:w-200 m-auto">
        <h1 class="text-center mb-4 text-2xl text-gray-800 font-bold">Import / Export Data</h1>
        <div class="flex flex-wrap items-center justify-center">

            <div
                class="p-1 text-gray-700"
            >
                <div class="tracking-tight text-center text-xl">Import Data</div>
                <div>
                    <textarea v-model="decodedData" class="w-128 h-32 border bg-white border-gray-400 rounded"></textarea>
                </div>
                <button class="border border-blue-400 rounded bg-blue-400 text-white p-2" value="" @click="importData()">Import data</button>

                <div class="tracking-tight text-center text-xl">Export Data</div>
                <p class="text-sm">The following string represents the data you have entered into the calculator.</p>
                <div>
                    <textarea class="w-128 h-32 border bg-white border-gray-400 rounded">{{encodedData}}</textarea>
                </div>
            </div>
        </div>
    </div>
</template>

<script>
export default {
    name: "import",
    props: [
        'library',
        'data'
    ],
    data() {
        return {
            decodedData: '',
        }
    },
    methods: {
        exportData()
        {
            this.$emit('saveLocalStorage');
        },
        importData()
        {
            try
            {
                let newData = JSON.parse(atob(this.decodedData))
                if(newData)
                {
                    this.$emit('saveLocalStorage', newData);
                    alert('Successfully imported data');
                }
            }
            catch(e)
            {
                alert('Unable to import data.')
            }

        }
    },
    computed: {
        encodedData()
        {
            return btoa(JSON.stringify(this.data));
        }
    }
}
</script>

<style scoped>

</style>
