<template>
    <div class="leaf">
        <h3>{{ value }}</h3>
        <button @click="validate(value)">Validate</button>
        <RandomValue 
            v-for="child in tree.children" 
            :key="child.value" 
            :tree="child" 
            :value="child.value" 
            :validate="validate"
        ></RandomValue>
    </div>
</template>

<script>
export default {
    name: 'RandomValue',
    props: {
        value: {
            type: String,
            required: true,
            default: ''
        },
        tree: {
            type: Object,
            required: false
        },
        validate: {
            type: Function,
            default: () => {}
        }
    }
}
</script>
<style>
.leaf {
    margin-left: 100px;
}
</style>