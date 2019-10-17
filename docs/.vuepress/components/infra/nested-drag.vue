<template>
    <draggable :class="{dragArea: true, root: level == 0}" tag="ul" :list="model" :group="{ name: 'g1' }">
        <li v-for="el in model" :key="el.domID" class="v-card">
            <v-toolbar
                  color="indigo"
                  dark
                >
                <v-toolbar-title>{{ el.name }}</v-toolbar-title>
                <v-spacer></v-spacer>
                <v-btn icon @click="removeItem(el.domID)">
                    <v-icon>mdi-delete</v-icon>
                </v-btn>
            </v-toolbar>

            <builder :builder_json="el" :builder_defaults="defaults" />
            <nested-drag :model="el.list" v-if="ableToHaveChildren(el)" :level="level + 1" />
        </li>
    </draggable>
</template>
<script>
import draggable from "vuedraggable";
import shortid from "shortid";
import {findIndex} from "lodash";
export default {
    props: {
        model: {
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
        },
        removeItem(domID) {
            console.log(domID);
            let index = findIndex(this.model, {domID: domID});
            if (index != -1) this.model.splice(index, 1);
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
    padding: 10px;
    margin-bottom: 10px;
}

</style>