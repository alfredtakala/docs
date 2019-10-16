<template>
    <draggable
        :list="list"
        v-bind="dragOptions"
        @start="drag = true"
        @end="drag = false"
        class="dragArea" :class="parentClass" :group="{ name: 'g1' }">
        {{level}}
        <div v-for="item in list" 
            :key="item.domID" class="child">
            <builder :builder_json="item" 
                :builder_defaults="defaults" />
            <nested-draggable :list="item.list" :level="level + 1"/>
            
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
        },
        level: {
            required: true, 
            type: Number
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
                /* animation: 200,
                disabled: false,
                ghostClass: "ghost" */
            };
        },
        parentClass() {
            if (this.level == 1) return "section";
            if (this.level == 2) return "box";
            if (this.level == 3) return "leaf";
        }
    }
};
</script>
<style scoped>
.dragArea {
    min-height: 50px;
}

.child {
    border: 1px solid blue;
}
.dragArea.section {
    outline: 2px solid;
    margin: 10px;
}
.dragArea.box {
    outline: 1px dashed;
    margin: 15px;
}
.dragArea.leaf {
    outline: 1px dotted;
    margin: 20px;
}
</style>