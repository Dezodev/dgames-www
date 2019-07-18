<template lang="html">
	<div class="">
		<a-row>
			<a-col :span="16">
				<h1 class="u-m-top-0">Jeu du pendu</h1>
			</a-col>
			<a-col :span="8" class="u-align-right">
				<a-button type="primary" @click="showWordModal">Nouvelle partie</a-button>
			</a-col>
		</a-row>

		<a-modal
			title="Choisissez un mot à faire découvrir."
			v-model="wordModalVisible"
			@ok="wordModalOk"
		>
			<a-input v-model="wordModal" placeholder="Inscriver votre mot ici"/>
		</a-modal>
	</div>
</template>

<script>
export default {
	data () {
		return {
			wordModalVisible: false,
			wordModal: null,
		};
	},
	methods: {
		showWordModal () {
			this.wordModalVisible = true
		},
		wordModalOk (ev) {
			this.wordModalVisible = false
		},
	},
}
</script>
