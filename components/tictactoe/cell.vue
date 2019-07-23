<template lang="html">
	<td :class="[
		'cell',
		{ 'highlight-cell': highlightCells.includes(cellKey) }
	]" @click="throwClick">
		<a-icon type="close" v-if="cells[cellKey] == 1" class="cell-mark" />
		<a-icon type="border" v-else-if="cells[cellKey] == 2" class="cell-mark" />
		<span v-else></span>
	</td>
</template>

<script>
export default {
	props: {
		cellKey: {
			type: Number,
		},
		cells: {
			type: Object,
			default () {
				return {}
			}
		},
		highlightCells: {
			type: Array,
			default () {
				return []
			}
		},
	},
	methods: {
		throwClick () {
			this.$emit('cellClick', this.cellKey)
		}
	}
}
</script>
