<template>
    <div>
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
    </div>
</template>
<script>
import Vuetify from 'vuetify';
import {filter, splice, cloneDeep} from 'lodash';
export default {
    name: "rdxToolbar",
    components: {
        Vuetify
    },
    props: ["model", "all_fields"],
    data() {
        let shortcut_fields = filter(this.all_fields, 'icon');
        return {
            shortcut_fields: shortcut_fields,
            openedFieldSelectionModal: false,
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
    methods: {
        // utility for 
        addFieldInstance(fieldType) {
            let instance = cloneDeep(fieldType);
            // generate UNIQUE ID
            instance.domID = Math.random().toString(36).substr(2, 9);
            this.model.push(instance);
        },
        // click Toolbak Icon results in new draggable element.
        onAddCommonFields(field) {
            this.addFieldInstance(field);
        },
        // Modal OK button click handler
        onAddFieldFromModal() {
            if (!this.modalSelectedFieldName) return;
            let selectedField = this.all_fields[this.modalSelectedFieldName]; // finds 
            if (!!selectedField) {
                this.addFieldInstance(selectedField);
                this.openedFieldSelectionModal = false; // close dialog
                this.modalSelectedFieldName = null; // reset
            }
        }
    }
}
</script>