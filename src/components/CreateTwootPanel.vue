<template
	><form
		class="create-twoot-panel"
		@submit.prevent="createNewTwoot"
		:class="{ '--exceeded': newTwootCharacterCount > 180 }"
	>
		<label for="newTwoot"><strong>New Twoot</strong> ({{ newTwootCharacterCount }}/180)</label>
		<textarea id="newTwoot" rows="4" v-model="state.newTwootContent" />

		<div class="create-twoot-panel__submit">
			<div class="create-twoot-type">
				<label for="newTwootType"><strong>Type: </strong></label>
				<select id="newTwootType" v-model="state.selectedTwootType">
					<option :value="option.value" v-for="(option, index) in state.twootTypes" :key="index">
						{{ option.name }}
					</option>
				</select>
			</div>

			<button>
				Twoot It!
			</button>
		</div>
	</form>
</template>

<script>
import { reactive, computed } from 'vue';

export default {
	name: 'CreateTwootPanel',

	setup(props, ctx) {
		const state = reactive({
			newTwootContent: '',
			selectedTwootType: 'instant',
			twootTypes: [
				{ value: 'draft', name: 'Draft' },
				{ value: 'instant', name: 'Instant Twoot' },
			],
		});

		const newTwootCharacterCount = computed(() => state.newTwootContent.length);

		function createNewTwoot() {
			if (state.newTwootContent && state.selectedTwootType !== 'draft') {
				ctx.emit('add-twoot', state.newTwootContent);
				state.newTwootContent = '';
			}
		}
	},
};
</script>

<style></style>
