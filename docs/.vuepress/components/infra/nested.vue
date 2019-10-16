<template>
    <draggable
        :list="list"
        v-bind="dragOptions"
        @start="drag = true"
        @end="drag = false">
    
        <div v-for="{item, i} in list"
            :key="i"> 
            {{i}}
            <builder :builder_json="item" :builder_defaults="defaults"  />
            
        </div>
        
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
                group: "description",
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