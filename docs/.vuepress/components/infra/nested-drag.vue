<template>
    <draggable :class="{dragArea: true, root: level == 0}" tag="ul" :list="list" :group="{ name: 'g1' }">
        <li v-for="el in list" :key="el.name" class="card">
            <p>{{ el.name }}</p>
            <builder :builder_json="el" :builder_defaults="defaults" />
            <nested-drag :list="el.list" v-if="ableToHaveChildren(el)" :level="level + 1" />
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
        },
        level: Number
    },
    components: {
        draggable
    },
    data() {
        return {
            defaults: {}
        }
    },
    computed: {
        dragAreaClass: function() {
            let classes = ["dragArea"];
            if (this.level === 0) classes.push("root");
            return classes.join(" ");
        }
    },
    methods: {
        ableToHaveChildren(element) {
            return (this.level < 2 && element.type === "section");
        }
    },
    name: "nested-drag"
};
</script>
<style scoped>
.dragArea {
    min-height: 80px;
    list-style: none;
    padding: 10px;
    border-top: 1px dashed #AAAAAA;
}
.dragArea.root {
    border-top: none;    
}

.dragArea li {
    -webkit-box-shadow: 0 2px 7px 0 rgba(0,0,0,.1);
    box-shadow: 0 2px 7px 0 rgba(0,0,0,.1);
    padding: 10px;
    margin-bottom: 10px;
}

</style>