<template>
    <div>
        <div>
            <p><strong>Money</strong></p>
            <p>Reserves: {{reserves}}</p>
            <p>Budget: {{budget}}</p>
            <p>Upkeep: {{upkeep}}</p>
        </div>
        <div>
            <p><strong>Soldiers</strong></p>
            <p>Infantry: {{infantry}}</p>
            <button v-on:click="hireInfantry">Recruit Infantry</button>
        </div>
        <div>
            <p><strong>Units</strong></p>
            <button v-on:click="createUnit">Create New Unit</button>
            <Unit v-for="unit in units" :key="unit.id"
                  v-bind:unit="unit"
                  v-on:unit-action="trainUnit"
            ></Unit>
        </div>
    </div>
</template>

<script>
    import Unit from "@/components/Unit";
    export default {
        name: "Game",
        components: {Unit},
        data: function() {
            return {
                        budget: 1,
                        reserves: 0,
                        infantry: 0,
                        salary: 0,
                        infantrySalary: 1,
                        units: {},
                        unitIndex: 1,

                    };
            },
        computed: {
            upkeep: function() {
                return this.salary;
            }
        },
        methods: {
            gameTick: function () {
                this.calcReserves()
                if(this.reserves < 0){
                    this.desert()
                }
            },
            startGame() {
                this.gameTimer = setInterval(()=> {this.gameTick()}, 1000)
            },
            calcReserves() {
                this.reserves += this.budget - this.upkeep;
            },
            hireInfantry() {
                if(this.reserves >= this.infantrySalary) {
                    this.infantry++;
                    this.salary += this.infantrySalary;
                }
            },
            loseInfantry()
            {
                if(this.infantry > 0) {
                    this.infantry--
                    this.salary -= this.infantrySalary;
                }
            },
            desert() {
              this.loseInfantry()
            },
            createUnit() {
                this.units[this.unitIndex] =
                    {
                        id: this.unitIndex,
                        name: this.unitIndex + 'st', //todo: add postfixes properly
                        experience: 0,
                        gear: 'none',
                        type: 'infantry',
                        soldiers: 0,
                        action: 'idle',
                        readiness: 0,
                    }
                this.unitIndex++
            },
            trainUnit(id, action){
                this.units[id].action = action
                console.log(action)
            }
        },
        mounted: function(){
            this.startGame()
        }
    }
</script>

<style scoped>

</style>