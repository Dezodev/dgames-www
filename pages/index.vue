<template>
	<div class="container">
		<h2>Liste des Jeux</h2>
	</div>
</template>

<script>
export default {
	data () {
		return {
			games_lists: [
				{
					id: 'hangman',
					label: 'Jeu du pendu'
				}
			]
		};
	}
}
</script>
