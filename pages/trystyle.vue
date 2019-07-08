<template lang="html">
	<div class="">
		<p>Lorem ipsum dolor sit amet, consectetur adipisicing elit. Consequuntur, libero, labore. Dolore suscipit iure veniam. Esse quod sapiente dolorem sequi rerum delectus eius obcaecati quam, itaque atque quidem fugit rem.</p>
		<p>Consectetur architecto, delectus non voluptas quae rem voluptatem distinctio quas voluptate ad excepturi ea doloremque qui minima quo, numquam assumenda iusto fugit ipsum sed dolorum eveniet. Asperiores optio ea quisquam?</p>

		<h2 id="buttons">Boutons</h2>

		<div>
			<a-button type="primary">Primary</a-button>
			<a-button>Default</a-button>
			<a-button type="dashed">Dashed</a-button>
			<a-button type="danger">Danger</a-button>
		</div>
		<div :style="{ marginTop: '20px' }">
			<a-button type="primary" ghost>Primary</a-button>
			<a-button ghost>Default</a-button>
			<a-button type="dashed" ghost>Dashed</a-button>
			<a-button type="danger" ghost>danger</a-button>
		</div>

		<h2>Breadcrumb</h2>

		<div class="mt-2">
			<a-breadcrumb>
				<a-breadcrumb-item>Home</a-breadcrumb-item>
				<a-breadcrumb-item><a href="">Application Center</a></a-breadcrumb-item>
				<a-breadcrumb-item><a href="">Application List</a></a-breadcrumb-item>
				<a-breadcrumb-item>An Application</a-breadcrumb-item>
			</a-breadcrumb>
		</div>

		<h2>Dropdown</h2>

		<div class="">
			<a-dropdown :trigger="['click']">
				<a class="ant-dropdown-link" href="#">
					Click me <a-icon type="down" />
				</a>
				<a-menu slot="overlay">
					<a-menu-item key="0">
						<a href="http://www.alipay.com/">1st menu item</a>
					</a-menu-item>
					<a-menu-item key="1">
						<a href="http://www.taobao.com/">2nd menu item</a>
					</a-menu-item>
					<a-menu-divider />
					<a-menu-item key="3">3rd menu item</a-menu-item>
				</a-menu>
			</a-dropdown>
		</div>

		<h2>Pagination</h2>

		<div class="">
			<a-pagination :value="3" :total="50" />
		</div>

		<h2>Steps</h2>
		<div>
			<a-steps :current="1">
				<a-step>
					<template slot="title">Finished</template>
					<span slot="description">This is a description.</span>
				</a-step>
				<a-step title="In Progress" description="This is a description." />
				<a-step title="Waiting" description="This is a description." />
			</a-steps>
		</div>


		h2{Steps}+div
	</div>
</template>

<script>
export default {
}
</script>

<style lang="css" scoped>
</style>
