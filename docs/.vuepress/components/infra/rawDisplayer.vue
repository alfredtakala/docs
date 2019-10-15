<template>
    <pre>{{ valueString }}</pre>
</template>
<script>
const props = {
    name: "raw-displayer",
    title: {
        required: true,
        type: String
    },
    value: {
        required: true
    }
};
export default {
    props,
    computed: {
        valueString() {
            return JSON.stringify(this.value, null, 2);
        }
    }
};
</script>
<style scoped>
pre {
    text-align: start;
    min-height: 200px;
    margin: 0;
    height: 100%;
    color: #ccc;
}
</style>