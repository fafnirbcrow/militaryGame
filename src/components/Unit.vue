<template>
    <div>
        <p>Unit Name: {{unit.name}}</p>
        <p>Unit Experience: {{unit.experience}}</p>
        <p>Unit Readiness: {{unit.readiness}}%</p>
        <p>Unit Gear: {{unit.gear}}</p>
        <p>Unit Type: {{unit.type}}</p>
        <p>Members: {{unit.soldiers}}</p>
        <p>Unit Action: {{unit.action}}</p>
        <button v-on:click="$emit('unit-action', unit.id,'train')">Train</button>

    </div>
</template>

<script>
    export default {
        name: "Unit",
        props: ['unit'],
    }
</script>

<style scoped>

</style>