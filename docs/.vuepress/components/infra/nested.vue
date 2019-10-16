<template>
    <draggable
        :list="list"
        v-bind="dragOptions"
        @start="drag = true"
        @end="drag = false"
        class="dragArea" :group="{ name: 'g1' }">
        <transition-group type="transition" :name="!drag ? 'flip-list' : null">
            <div v-for="item in list" 
                :key="item.domID">
                <builder :builder_json="item" 
                    :builder_defaults="defaults" />
                <template v-if="item && item.list && item.list.length > 0">
                    <nested-draggable :list="item.list" />
                </template>
            </div>
        </transition-group>
    </draggable>
    
</template>
<script>
import draggable from "vuedraggable";
export default {
    name: "nested-draggable",
    props: {
        list: {
            required: true,
            type: Array
        }
    },
    data () {
        return {
            drag: false,
            defaults: {}
        }
    },
    components: {
        draggable
    },
    computed: {
        // to add transition while dragging
        dragOptions() {
            return {
                animation: 200,
                disabled: false,
                ghostClass: "ghost"
            };
        }
    }
};
</script>
<style scoped>
.dragArea {
    min-height: 50px;
    outline: 1px dashed;
}
</style>