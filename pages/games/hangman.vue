<template lang="html">
	<div id="page-hangman-index">
		<div class="row">
			<div class="col-xs-8">
				<h1 class="u-m-top-0">Jeu du pendu</h1>
			</div>
			<div class="col-xs-4 u-align-right">
				<a-button type="primary" @click="showWordModal">Nouvelle partie</a-button>
			</div>
		</div>

		<div class="hangman-game game">
			<div class="hangman-word" v-if="word_to_find">
				<ul class="list-inline">
					<li :class="[
						'one-letter','list-inline-item',
						{ 'letter-founded': (letters_founded.includes(l)) }
					]" v-for="l in word_to_find">
						<span v-if="letters_founded.includes(l)">{{ l }}</span>
						<span v-else>&nbsp;</span>
					</li>
				</ul>

				<p class="u-align-center" v-if="game_lost">Mot à trouver : {{ word_to_find }}</p>
			</div>

			<div class="hangman-letter-btns">
				<div class="row between-xs" v-for="(ls, ind) in azerty_letters" :key="'ls-azerty-'+ind">
					<div class="col-xs" v-for="l in ls" :key="'l-azerty-'+l">
						<div @click="letterChoose(l)" :class="['one-letter', {
							'letter-founded': (letters_founded.includes(l)),
							'letter-error': (letters_error.includes(l)),
							'disable': (letters_founded.includes(l) || letters_error.includes(l) || !is_game_started)
						}]">{{ l }}</div>
					</div>
				</div>
			</div>

			<div class="row">
				<div class="col-xs-6">
					<a-card
						class="hangman-letter-error"
						title="Liste des mauvaise lettres"
						:bordered="false">
						<p class="letter-list">{{ all_letters_error }}</p>
					</a-card>
				</div>
				<div class="col-xs-6 u-align-center">
					<a-progress type="circle" :percent="lifePercent" :format="lifeProgressText"/>
				</div>
			</div>
		</div>

		<a-modal
			title="Choisissez un mot à faire découvrir."
			v-model="wordModalVisible"
		>
			<a-input v-model="wordModal" placeholder="Inscriver votre mot ici"/>

			<div class="u-d-flex" slot="footer">
				<a-button class="u-m-right-auto" @click="getRandomWord">Mot aléatoire</a-button>
				<a-button key="back" @click="hideWordModal">Annuler</a-button>
				<a-button key="submit" type="primary" @click="wordModalOk">
					OK
				</a-button>
			</div>
		</a-modal>
	</div>
</template>

<script>
import words from "an-array-of-french-words"
import _ from 'lodash'

export default {
	data () {
		return {
			wordModalVisible: false,
			wordModal: null,

			fr_words: [],
			word_to_find: null,

			letters_to_find: [],
			letters_founded: [],
			letters_error: [],

			remaining_lives: 11,
			total_lives: 11,

			is_game_started: false,

			azerty_letters: [
				"azertyuiop",
				"qsdfghjklm",
				"wxcvbn"
			]
		};
	},
	mounted () {
		this.fr_words = _.filter(words, function(s) { return s.length > 5; });
	},
	methods: {
		showWordModal () {
			this.wordModalVisible = true
		},
		hideWordModal () {
			this.wordModalVisible = false
		},
		wordModalOk (ev) {
			this.hideWordModal()

			this.word_to_find = _.deburr(_.toLower(this.wordModal))
			this.wordModal = null
			this.startGame();
		},
		getRandomWord () {
			this.wordModal = _.sample(this.fr_words);
		},
		startGame () {
			let this_word = _.toLower(this.word_to_find),
				word_in_arr = _.split(this_word, '')

			// Reinit. vars
			this.letters_to_find = [];
			this.letters_founded = [];
			this.letters_error = [];

			this.letters_to_find = _.uniq(word_in_arr)
			this.letters_founded.push(
				_.head(word_in_arr),
				_.last(word_in_arr)
			)

			this.is_game_started = true
			this.remaining_lives = 11
		},
		letterChoose (l) {
			// Break if no word are specified
			if (!this.is_game_started) return false

			// Break if the users have no life
			if (this.remaining_lives == 0) return false

			// Break if this letter is already choose
			if (this.letters_founded.includes(l) || this.letters_error.includes(l))
				return false;

			if (this.letters_to_find.includes(l)) {
				this.letters_founded.push(l)
			} else {
				this.letters_error.push(l)
				if (this.remaining_lives > 0) this.remaining_lives--
			}

			if (this.is_all_letters_founded) {
				this.is_game_started = false

				this.$notification.open({
					message: 'Bravo !!',
					description: 'Vous venez de trouver le mot.',
					icon: <i class="em em-clap"/>
				});
			} else if (this.remaining_lives == 0) {
				this.is_game_started = false

				this.$notification.open({
					message: "Dommage.",
					description: 'Vous n\'avais pas réussi à trouver le mot. Vous pouvez recommencer une nouvelle partie',
					icon: <i class="em em-frowning"/>
				});
			}
		},
		lifeProgressText () {
			return `${this.remaining_lives} / 11 vie(s)`
		},
	},
	computed: {
		is_all_letters_founded () {
			return _.isEqual(_.sortBy(this.letters_founded), _.sortBy(this.letters_to_find));
		},
		all_letters_error () {
			return _.join(this.letters_error, ', ')
		},
		lifePercent () {
			return (this.remaining_lives / this.total_lives) * 100
		},
		game_lost () {
			if (this.remaining_lives == 0 && !this.is_all_letters_founded) {
				return true;
			} else {
				return false;
			}
		}
	},
	head: {
		title: 'Jeu du pendu',
	}
}
</script>
