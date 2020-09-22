<template>
    <div class="leaf">
        <h3>{{ value }}</h3>
        <button @click="validate(value)">Validate</button>
        <RandomValue 
            v-for="child in tree.children" 
            :key="child.value" 
            :tree="child" 
            :value="child.value"
            :depth="child.depth"
        ></RandomValue>
    </div>
</template>

<script>
import { bus } from '@/main'

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
        depth: {
            type: Number
        }
    },
    methods: {
        handleValidate() {
            console.log(this.value)
        },
        validate() {
            bus.$emit('onValidateComponent', this.depth)
        }
    },
    created() {
        bus.$on('onValidateComponent', depth => {
            if(depth <= this.depth)
            this.handleValidate()
        })
    }
}
</script>
<style>
.leaf {
    margin-left: 100px;
}
</style>