<template>
    <draggable class="dragArea" tag="ul" :list="list" :group="{ name: 'g1' }">
        <li v-for="el in list" :key="el.name">
            <p>{{ el.name }}</p>
            <builder :builder_json="el" :builder_defaults="defaults" />
            <nested-drag :list="el.list" />
        </li>
    </draggable>
</template>
<script>
import draggable from "vuedraggable";
export default {
    props: {
        list: {
            required: true,
            type: Array
        }
    },
    components: {
        draggable
    },
    data() {
        return {
            defaults: {}
        }
    },
    name: "nested-drag"
};
</script>
<style scoped>
.dragArea {
    min-height: 50px;
    outline: 1px dashed;
}
</style>