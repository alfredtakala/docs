<template>
    <v-app>
        <v-toolbar dense>
            <toolbar :model="list" :all_fields="all_fields" />           
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
    components: {
        Vuetify,
        toolbar,
        draggable,
        builder,
        rawDisplayer
    },
    props: ['field'],
    data() {
        return {
            all_fields: this.$attrs.bundled_fields,
            defaults: {},
            drag: false, // fields specifing dragging status
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
        
    }
};
</script>
<style scoped></style>