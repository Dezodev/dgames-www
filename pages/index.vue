<template>
	<div class="container">
		<h2>Liste des Jeux</h2>

		<div class="row">
			<div class="col-xs-4" v-for="gam in games_lists" :key="'game_' + gam.id">
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
			</div>
		</div>
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
					description: '',
					route: '/games/hangman'
				},
				{
					id: 'tictactoe',
					label: 'Tic tac toe',
					description: '',
					route: '/games/tictactoe'
				},
			]
		};
	}
}
</script>
