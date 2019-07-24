<template lang="html">
	<div id="page-tictactoe-index">
		<div class="row">
			<div class="col-xs-8">
				<h1 class="u-m-top-0">Tic tac toe</h1>
			</div>
			<div class="col-xs-4 u-align-right">
				<a-button type="primary" @click="showNewGameModal">Nouvelle partie</a-button>
			</div>
		</div>

		<div class="tictactoe-game game">
			<div class="row players-disp">
				<div :class="['col-xs-6', 'one-player', {
					'curr-player': activePlayer == 1
				}]">
					<p class="player-name">
						<a-icon type="close" class="u-m-right-sm" />
						{{ players[1].name }} - <span class="player-score">{{ players[1].score }}</span>
					</p>
				</div>
				<div :class="['col-xs-6', 'one-player', {
					'curr-player': activePlayer == 2
				}]">
					<p class="player-name">
						<a-icon type="border" class="u-m-right-sm" />
						{{ players[2].name }} - <span class="player-score">{{ players[2].score }}</span>
					</p>
				</div>
			</div>

			<table class="grid">
				<tbody>
					<tr>
						<tictactoeCell
							:cellKey="1"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
						<tictactoeCell
							:cellKey="2"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
						<tictactoeCell
							:cellKey="3"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
					</tr>
					<tr>
						<tictactoeCell
							:cellKey="4"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
						<tictactoeCell
							:cellKey="5"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
						<tictactoeCell
							:cellKey="6"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
					</tr>
					<tr>
						<tictactoeCell
							:cellKey="7"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
						<tictactoeCell
							:cellKey="8"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
						<tictactoeCell
							:cellKey="9"
							:cells="cells"
							:highlightCells="highlightCells"
							@cellClick="markCell"
						></tictactoeCell>
					</tr>
				</tbody>
			</table>

			<p class="player-win u-align-center" v-if="gameStatus == 'win' && players[activePlayer]">
				<b>{{ players[activePlayer].name }}</b> a gagné&centerdot;e cette partie.

				<a-button class="u-m-left-sm" @click="startGame(activePlayer)">Continuer</a-button>
			</p>
			<p class="players-draw u-align-center" v-if="gameStatus == 'draw'">
				Vous êtes à égaliter sur cette partie.

				<a-button class="u-m-left-sm" @click="startGame(activePlayer)">Continuer</a-button>
			</p>
		</div>

		<a-modal
			title="Basic Modal"
			v-model="newGameModVisible"
			@ok="newGame"
			okText="Commencer"
			cancelText="Annuler"
		>
			<a-form layout="vertical">
				<a-form-item label="Nom du Joueur 1">
					<a-input v-model="players[1].name" placeholder="Nom du Joueur 1" />
				</a-form-item>

				<a-form-item label="Nom du Joueur 2">
					<a-input v-model="players[2].name" placeholder="Nom du Joueur 2" />
				</a-form-item>
			</a-form>
		</a-modal>
	</div>
</template>

<script>
import tictactoeCell from '~/components/tictactoe/cell'

export default {
	components: {
		tictactoeCell
	},
	data () {
		return {
			players: {
				1: {
					name: 'Joueur 1',
					score: 0,
				},
				2: {
					name: 'Joueur 2',
					score: 0,
				},
			},

			activePlayer: 0,
			nbMove: 0,
			gameStatus: 'stop',

			cells: {
				1: 0, 2: 0, 3: 0,
				4: 0, 5: 0, 6: 0,
				7: 0, 8: 0, 9: 0
			},
			highlightCells: [],

			// contains all (8) possible winning conditions
			winConditions: [
				[1, 2, 3], [4, 5, 6], [7, 8, 9], // rows
				[1, 4, 7], [2, 5, 8], [3, 6, 9], // columns
				[1, 5, 9], [3, 5, 7]             // diagonals
			],

			newGameModVisible: false,
		}
	},
	methods: {
		showNewGameModal () {
			this.newGameModVisible = true
		},
		newGame() {
			this.players[1].score = 0
			this.players[2].score = 0

			this.startGame();
		},
		startGame (next_player = 1) {
			// Reinit vars
			this.activePlayer = 0
			this.nbMove = 0
			this.highlightCells = []

			this.cells = {
				1: 0, 2: 0, 3: 0,
				4: 0, 5: 0, 6: 0,
				7: 0, 8: 0, 9: 0
			}

			// set current player
			this.activePlayer = next_player
			this.gameStatus = 'play'

			this.newGameModVisible = false
		},
		markCell (cellKey) {
			if (this.gameStatus == 'stop') {
				return this.$notification.warning({
					message: 'La partie n\'est pas commencé',
					description: 'Pour commencer une partie, vous devez cliquer sur le bouton "Nouvelle partie".'
				})
			} else if (this.gameStatus != 'play') {
				return false
			}

			this.nbMove++;

			if (
				[1, 2].includes(this.activePlayer) &&
				cellKey >= 1 && cellKey <= 9 &&
				this.cells[cellKey] == 0
			) {
				this.cells[cellKey] = this.activePlayer

				if (this.checkForWin()) {
					let player_win = this.activePlayer

					this.players[player_win].score++
					this.gameStatus = 'win'
				} else if (this.nbMove >= 9) {
					this.players[1].score++
					this.players[2].score++

					this.gameStatus = 'draw'
				}else {
					this.activePlayer = (this.activePlayer == 1) ? 2 : 1;
				}

			}
		},
		checkForWin () {
			for (let one_cond of this.winConditions) {
				// compares 3 cell values based on the cells in the condition
				if (this.areEqual(
					this.cells[one_cond[0]],
					this.cells[one_cond[1]],
					this.cells[one_cond[2]],
				)) {
					this.highlightCells = one_cond
					return true
				}
			}

			return false
		},
		nextRound () {
			this.startGame(pl_win)
		},
		areEqual () {
			var len = arguments.length;

			// loops through each value and compares them with an empty sting and
			// for inequality
			for (var i = 1; i < len; i++){
				if (arguments[i] === 0 || arguments[i] !== arguments[i-1]) return false;
			}

			return true;
		},
	},
	head: {
		title: 'Tic tac toe',
	}
}
</script>
