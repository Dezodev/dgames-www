<template>
	<div id="default-layout">
		<a-layout>
			<a-layout-sider>
				<h1>DGames</h1>

			</a-layout-sider>

			<a-layout>
				<a-layout-content>
					<nuxt></nuxt>
				</a-layout-content>

				<a-layout-footer :style="{ textAlign: 'center' }">
					DGames &copy; 2019 &ndash; Développer par <a href="https://dezodev.tk" target="_blank">Dezodev</a>
				</a-layout-footer>
			</a-layout>
		</a-layout>
	</div>
</template>

<script>
export default {
}
</script>
