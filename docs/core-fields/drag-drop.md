# Drag & Drop

## Example Declaration
<script>
import aceEditor from './ace-editor.json';
import background from './background.json';

let bundledFields = {};
bundledFields['aceEditor'] = aceEditor;
bundledFields['background'] = background;

export default {
    data () {
        return {
            bundledFields: bundledFields,
            defaults: {}
        };
    }
}
</script>
<drag :bundled_fields="bundledFields" :builder_defaults="defaults" />
