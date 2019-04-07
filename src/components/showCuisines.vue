<template>
    <div id="cuis">
        <div v-for="cuisin in selectedCuisines" :key="cuisin" @click="replaceCuisine(cuisin)" id="h">
            {{cuisin}}<br>
        </div>
    </div>
</template>

<script>
export default {
    props: ["cuisine"],
    data() {
        return {
            selectedCuisines: [],
            cuisines: require('../data/Cuisines.js')
        }
    },
    methods: {
        replaceCuisine(val){
            console.log(val)
            this.$emit('replaceCuisine', val);
        }
    },
    watch: {
        cuisine: function () {
            this.selectedCuisines = []            
            this.cuisines.forEach(cuis => {
                if(cuis.toUpperCase().includes(this.cuisine.toUpperCase())){
                    this.selectedCuisines.push(cuis);
                }
            });
            console.log(this.selectedCuisines)
        }
    }
}
</script>

<style>
#cuis {
    overflow-y: scroll;
    height: 15vh;
    border: 2px solid #ddd;
    width: 30vw;
    background-color: #f6f6f6;
    margin-left: 37%;
    float: left;
}
#h:hover {background-color: #806f6f}
</style>