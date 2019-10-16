<template>
    <v-app>
        <v-toolbar dense>
            <rdx-toolbar :model="list" :all_fields="all_fields" />           
        </v-toolbar>
        <v-row class="panel-row">
            <v-col cols sm="12" md="7" class="builder-panel">
                <div>
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
                </div>
            </v-col>
            <v-col cols sm="12" md="5">
                <rawDisplayer :value="list" title="List" />
            </v-col>
        </v-row>
        <v-row>
            <v-col cols sm="12">
                
            </v-col>
        </v-row>
    </v-app>
</template>

<script>
import Vuetify from 'vuetify';
import draggable from "vuedraggable";
import builder from "./builder.vue";
import rawDisplayer from "./infra/rawDisplayer";
import rdxToolbar from "./rdxToolbar.vue";
import nestedDraggable from "./infra/nested";
export default {
    name: "rdxDrag",
    components: {
        Vuetify,
        rdxToolbar,
        draggable,
        builder,
        rawDisplayer,
        nestedDraggable
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
<style scoped>
    .v-toolbar {
        max-height: 48px;
    }
    .panel-row {
        height: 300px;
        margin-top: 5px;        
    }
    .panel-row > div {
        padding-top: 0px;
        padding-bottom: 0px;
    }
    @media (min-width: 768px) {
        .builder-panel {
            margin-left: 15px;
            margin-right: -15px;
            padding-left: 0px;
            padding-right: 0px;
        }
    }
    
    .builder-panel {
        min-height: 250px;
    }
    .builder-panel > div:first-child {
        background: #F1F1F1;
        height: 100%;
    }
</style>