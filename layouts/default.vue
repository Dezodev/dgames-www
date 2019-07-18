<template>
	<div id="default-layout">
		<a-layout>
			<a-layout-sider :width="300">
				<h1 class="u-m-top-0">DGames</h1>

				<a-menu theme="dark" :selectedKeys="currentMenu" mode="inline">
					<a-menu-item v-for="it in menuItems" :key="it.key">
						<nuxt-link :to="it.route">
							<a-icon v-if="it.aIcon" :type="it.aIcon" />
							<i v-else-if="it.faIcon" :class="[it.faIcon, 'menu-icon']"></i>
							<img v-else-if="it.imgIcon" :src="it.imgIcon" class="menu-icon">

							<span>{{ it.label }}</span>
						</nuxt-link>
					</a-menu-item>
				</a-menu>
			</a-layout-sider>

			<a-layout>
				<a-layout-content>
					<nuxt></nuxt>
				</a-layout-content>

				<a-layout-footer :style="{ textAlign: 'center' }">
					DGames &copy; 2019 &ndash; <a href="https://dezodev.tk" target="_blank">Développé par Dezodev</a>
				</a-layout-footer>
			</a-layout>
		</a-layout>
	</div>
</template>

<script>
import lodash from 'lodash'

export default {
	data () {
		return {
			menuItems: [
				{
					key: 'home',
					label: 'Accueil',
					route: '/',
					aIcon: false,
					faIcon: 'fas fa-home',
					imgIcon: false,
				},
				{
					key: 'hangman',
					label: 'Jeu du pendu',
					route: '/games/hangman',
					aIcon: false,
					faIcon: 'fas fa-font',
					imgIcon: false,
				},
				{
					key: 'trystyle',
					label: 'Styles',
					route: '/trystyle',
					aIcon: false,
					faIcon: 'fas fa-paint-brush',
					imgIcon: false,
				},
			],
			currentMenu: [],
		};
	},
	mounted () {
		// Get current menu
		this.searchCurrRoute()
	},
	methods: {
		searchCurrRoute () {
			let itemFound = _.find(this.menuItems, ['route', this.$nuxt.$route.path]);

			if(!_.isEmpty(itemFound)) this.currentMenu = [itemFound.key]
		},
	},
	watch: {
		'$route.path': function() {
			// Change current menu
			this.searchCurrRoute()
		}
	},
}
</script>
