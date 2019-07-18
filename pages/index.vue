<template>
	<div class="container">
		<h2>Liste des Jeux</h2>

		<a-row>
			<a-col :span="8" v-for="gam in games_lists" :key="gam.id">
				<a-card>
					<a-card-meta
						:title="gam.label"
						:description="gam.description"
						:style="{ marginBottom: '10px' }">
					</a-card-meta>
					<nuxt-link :to="gam.route">
						<a-button type="primary">Jouer <i class="fas fa-gamepad u-m-left-md"></i></a-button>
					</nuxt-link>
				</a-card>
			</a-col>
		</a-row>
	</div>
</template>

<script>
export default {
	data () {
		return {
			games_lists: [
				{
					id: 'hangman',
					label: 'Jeu du pendu',
					description: 'Jouer pour trouver le mot choisi.',
					route: '/games/hangman'
				}
			]
		};
	}
}
</script>
