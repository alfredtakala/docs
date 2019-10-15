<template>
    <v-app>
        <v-toolbar dense>
            <v-tooltip bottom v-for="field in shortcut_fields" >
                <template v-slot:activator="{ on : openTooltip }">
                    <v-btn icon v-on="openTooltip" color="primary" @click="onAddCommonFields(field)">
                        <v-icon>{{ field.icon }}</v-icon>
                    </v-btn>
                </template>
                <span> {{ field.name }} </span>
            </v-tooltip>
            <v-tooltip bottom>
                <template v-slot:activator="{on : openTooltip}">
                    <v-btn color="primary" icon v-on:click="openedFieldSelectionModal = true" v-on="openTooltip">
                        <v-icon>mdi-plus-circle-outline</v-icon>
                    </v-btn>
                </template>
                <span>Add Field</span>
            </v-tooltip>
            <v-dialog v-model="openedFieldSelectionModal" max-width="600px">
                <v-card>
                    <v-card-title>
                        <span class="headline">Add Field</span>
                    </v-card-title>
                    <v-card-text>
                        <v-autocomplete
                          v-model="modalSelectedFieldName"
                          :items="allGroupedFields"
                          filled
                          clearable
                          solo
                          color="blue-grey lighten-2"
                          label="Select"
                          item-text="title"
                          item-value="model"
                        >
                            <template v-slot:selection="data">
                                <v-chip
                                    v-bind="data.attrs"
                                    :input-value="data.selected"
                                    class="white--text"
                                    color="blue-grey"
                                >
                                    {{ data.item.title }}
                                </v-chip>
                            </template>
                            <template v-slot:item="data">
                                <v-list-item-content v-text="data.item.title"></v-list-item-content>
                            </template>
                        </v-autocomplete>
                    </v-card-text>
                    <v-card-actions>
                        <v-spacer></v-spacer>
                        <v-btn color="blue darken-1" text @click="openedFieldSelectionModal = false">Cancel</v-btn>
                        <v-btn color="blue darken-1" text @click="onAddFieldFromModal">Add</v-btn>
                    </v-card-actions>
                </v-card>
            </v-dialog>
            
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
import {filter, splice, cloneDeep} from 'lodash';
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
        let shortcut_fields = filter(this.$attrs.bundled_fields, 'icon');
        return {
            shortcut_fields: shortcut_fields,
            defaults: {},
            drag: false, // fields specifing dragging status
            openedFieldSelectionModal: false,
            list: [],
            modalSelectedFieldName: null,
            allGroupedFields: [
                { header: 'Group 1' },
                { title: 'Ace Editor', model: 'aceEditor' },
                { title: 'Background', model: 'background' },
                { divider: true },
                { header: 'Color' },
                { title: 'Color Gradient', model: 'colorGradient' },
                { title: 'Color RGBA', model: 'colorRGBA' },
                { title: 'Color', model: 'color' }
            ],
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
        },
        allSupportedFields() {
            return this.$attrs.bundled_fields;
        }
    },
    methods: {
        // utility for 
        addFieldInstance(fieldType) {
            let instance = cloneDeep(fieldType);
            // generate UNIQUE ID
            instance.domID = Math.random().toString(36).substr(2, 9);
            this.list.push(instance);
        },
        // click Toolbak Icon results in new draggable element.
        onAddCommonFields(field) {
            this.addFieldInstance(field);
        },
        // Modal OK button click handler
        onAddFieldFromModal() {
            if (!this.modalSelectedFieldName) return;
            let selectedField = this.allSupportedFields[this.modalSelectedFieldName]; // finds 
            if (!!selectedField) {
                this.addFieldInstance(selectedField);
                this.openedFieldSelectionModal = false; // close dialog
                this.modalSelectedFieldName = null; // reset
            }
        }
    }
};
</script>
<style scoped></style>