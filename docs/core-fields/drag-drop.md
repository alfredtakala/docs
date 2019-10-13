# Drag & Drop

## Example Declaration
<script>
import aceEditor from './ace-editor.json';
import background from './background.json';
import border from './border.json';
import buttonSet from './button-set.json';
import checkbox from './checkbox.json';
import colorGradient from './color-gradient.json';
import colorRGBA from './color-rgba.json';
import color from './color.json';
import date from './date.json';
import dimensions from './dimensions.json';
import divide from './divide.json';
import editor from './editor.json';
import gallery from './gallery.json';
import imageSelect from './image-select.json';
import info from './info.json';
import linkColor from './link-color.json';
import media from './media.json';
import multiText from './multi-text.json';
import paletteColor from './palette-color.json';
import password from './password.json';
import radio from './radio.json';
import raw from './raw.json';
import section from './section.json';
import selectImage from './select-image.json';
import select from './select.json';
import slider from './slider.json';
import slides from './slides.json';
import sortable from './sortable.json';
import sorter from './sorter.json';
import spacing from './spacing.json';
import spinner from './spinner.json';
import switchJSON from './switch.json';
import text from './text.json';
import textarea from './textarea.json';
import typography from './typography.json'; 

let bundledFields = {};
bundledFields['aceEditor'] = aceEditor;
bundledFields['background'] = background;
bundledFields['border'] = border;
bundledFields['buttonSet'] = buttonSet;
bundledFields['checkbox'] = checkbox;
bundledFields['colorGradient'] = colorGradient;
bundledFields['colorRGBA'] = colorRGBA;
bundledFields['color'] = color;
bundledFields['date'] = date;
bundledFields['dimensions'] = dimensions;
bundledFields['divide'] = divide;
bundledFields['editor'] = editor;
bundledFields['gallery'] = gallery;
bundledFields['imageSelect'] = imageSelect;
bundledFields['info'] = info;
bundledFields['linkColor'] = linkColor;
bundledFields['media'] = media;
bundledFields['multiText'] = multiText;
bundledFields['paletteColor'] = paletteColor;
bundledFields['password'] = password;
bundledFields['radio'] = radio;
bundledFields['raw'] = raw;
bundledFields['section'] = section;
bundledFields['selectImage'] = selectImage;
bundledFields['select'] = select;
bundledFields['slider'] = slider;
bundledFields['slides'] = slides;
bundledFields['sortable'] = sortable;
bundledFields['sorter'] = sorter;
bundledFields['spacing'] = spacing;
bundledFields['spinner'] = spinner;
bundledFields['switchJSON'] = switchJSON;
bundledFields['text'] = text;
bundledFields['textarea'] = textarea;
bundledFields['typography'] = typography;

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
