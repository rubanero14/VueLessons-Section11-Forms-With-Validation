<template>
    <ul>
        <li :class="{active: modelValue === 'poor'}"><button type="button" @click="activate('poor')">Poor</button></li>
        <li :class="{active: modelValue === 'average'}"><button type="button" @click="activate('average')">Average</button></li>
        <li :class="{active: modelValue === 'great'}"><button type="button" @click="activate('great')">Great</button></li>
    </ul>
</template>

<script>
export default {
    props: ['modelValue'],
    emits: ['update:modelValue'],
    methods: {
        activate(option){
            this.$emit('update:modelValue', option)
        }
    },
}
</script>


<style scoped>
.active button {
    border-color: #a00078;
    color: #a00078;
}

ul {
    list-style: none;
    margin: 0.5rem 0;
    padding: 0;
    display: flex;
}

li {
    margin: 0 1rem;
    display: flex;
    justify-content: center;
    align-items: center;
}

li button {
    font: inherit;
    border: 1px solid #ccc;
    background: transparent;
    cursor: pointer;
    border-radius: 5px;
    padding: 0.25rem 0.75rem;
}
</style>