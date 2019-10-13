<template>
    <v-app>
        <v-toolbar dense>
            <v-btn icon v-for="field in fields" @click="onToolbaIconClick(field)">
                <v-icon>{{ field.icon }}</v-icon>
            </v-btn>
        </v-toolbar>
        <v-row>
            <v-col class="text-center" cols="12" sm="8">
                <draggable
                    :list="list"
                    v-bind="dragOptions"
                    @start="drag = true"
                    @end="drag = false">
                    <transition-group type="transition" :name="!drag ? 'flip-list' : null">
                        <builder :builder_json="item" 
                            v-for="item in list"
                            :key="item.domID"
                            :builder_defaults="defaults" />
                    </transition-group>
                </draggable>
            </v-col>
            <v-col cols="12" sm="4">
                <rawDisplayer :value="list" title="List" />
            </v-col>
        </v-row>
    </v-app>
</template>

<script>
import Vuetify from 'vuetify';
import draggable from "vuedraggable";
import builder from "./builder.vue";
import rawDisplayer from "./infra/rawDisplayer";
export default {
    name: "third-party",
    display: "Third party",
    order: 10,
    components: {
        Vuetify,
        draggable,
        builder,
        rawDisplayer
    },
    props: ['field'],
    data() {
        let bundled_fields = this.$attrs.bundled_fields;
        return {
            fields: bundled_fields,
            defaults: {},
            drag: false,
            list: []
        };
    },
    computed: {
        // to add transition while dragging
        dragOptions() {
            return {
                animation: 200,
                group: "description",
                disabled: false,
                ghostClass: "ghost"
            };
        }
    },
    methods: {
        inputChanged(val) {
            this.activeNames = val;
        },
        // click Toolbak Icon results in new draggable element.
        onToolbaIconClick(field) {
            field.domID = Math.random().toString(36).substr(2, 9);
            this.list.push(field);
        }
    }
};
</script>
<style scoped></style>