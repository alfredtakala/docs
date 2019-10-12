<template>
	<div class="row">
		<div class="col-8">
			<draggable
				:list="list"
				:component-data="collapseComponentData">
				<builder :builder_json="tags"           
						v-for="item in list"
						:key="item.id"
						:builder_defaults="defaults" />
			</draggable>
			<div class="v-application">
				<div class="v-application--wrap">
					<v-row justify="space-around">
					    <v-icon large color="green darken-2">mdi-domain</v-icon>

					    <v-icon large color="blue darken-2">mdi-message-text</v-icon>

					    <v-icon large color="purple darken-2">mdi-dialpad</v-icon>

					    <v-icon large color="teal darken-2">mdi-email</v-icon>

					    <v-icon large color="blue-grey darken-2">mdi-call-split</v-icon>

					    <v-icon large color="orange darken-2">mdi-arrow-up-bold-box-outline</v-icon>
					  </v-row>
					<v-alert
				      dense
				      text
				      type="success"
				    >
				      I'm a dense alert with the <strong>text</strong> prop and a <strong>type</strong> of success
				    </v-alert>
				    <v-row align="center">
					    <v-col class="text-center" cols="12" sm="4">
					      <div class="my-2">
					        <v-btn small>Normal</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn small color="primary">Primary</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn small color="error">Error</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn small disabled>Disabled</v-btn>
					      </div>
					    </v-col>
					    <v-col class="text-center" cols="12" sm="4">
					      <div class="my-2">
					        <v-btn>Normal</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn color="primary">Primary</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn color="error">Error</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn disabled>Disabled</v-btn>
					      </div>
					    </v-col>
					    <v-col class="text-center" cols="12" sm="4">
					      <div class="my-2">
					        <v-btn large>Normal</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn large color="primary">Primary</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn large color="error">Error</v-btn>
					      </div>
					      <div class="my-2">
					        <v-btn large disabled>Disabled</v-btn>
					      </div>
					    </v-col>
					  </v-row>
				</div>
			</div>
		</div>
		<rawDisplayer class="col-4" :value="list" title="List" />
	</div>
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
		console.log(bundled_fields);
		return {
			tags: bundled_fields['background'],
			defaults: {},
			list: [
				{
					title: "Consistency",
					id: 1,
					text: [
						"Consistent with real life: in line with the process and logic of real life, and comply with languages and habits that the users are used to;",
						"Consistent within interface: all elements should be consistent, such as: design style, icons and texts, position of elements, etc."
					]
				},
				{
					title: "Feedback",
					id: 2,
					text: [
						"Operation feedback: enable the users to clearly perceive their operations by style updates and interactive effects;",
						"Visual feedback: reflect current state by updating or rearranging elements of the page."
					]
				},
				{
					title: "Efficiency",
					id: 3,
					text: [
						"Simplify the process: keep operating process simple and intuitive;",
						"Definite and clear: enunciate your intentions clearly so that the users can quickly understand and make decisions;",
						"Easy to identify: the interface should be straightforward, which helps the users to identify and frees them from memorizing and recalling."
					]
				},
				{
					title: "Controllability",
					id: 4,
					text: [
						"Decision making: giving advices about operations is acceptable, but do not make decisions for the users;",
						"Controlled consequences: users should be granted the freedom to operate, including canceling, aborting or terminating current operation."
					]
				}
			],
			activeNames: [1],
			collapseComponentData: {
				on: {
					input: this.inputChanged
				},
				props: {
					value: this.activeNames
				}
			}
		};
	},
	methods: {
		inputChanged(val) {
			this.activeNames = val;
		}
	}
};
</script>
<style scoped></style>