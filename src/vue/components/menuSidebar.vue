
<template>
	<aside class="column is-2 menu" aria-label="main navigation">
		<img class="menu-logo" src="/src/static/img/logo_flat.png" alt="logo TV Time" />
		<div v-if="this.$route.name === 'list'"
			 class="menu-item control has-icons-left has-icons-right">
			<input class="input is-small" v-model="search" type="text" @change="saveSearch" placeholder="Search">
			<span class="icon is-small is-right">
    			<i class="fas fa-search"></i>
  			</span>
		</div>
		<ul class="menu-item menu-list">
			<li><router-link :to="{ path : '/' }"><i class="fas fa-compass"></i>Explore</router-link></li>
			<template v-if="$route.name === 'list'">
				<li><a v-on:click="openAddSidebar"><i class="fas fa-film"></i>Add movie</a></li>
			</template>
			<template v-else-if="$route.name === 'details'">
				<li><a v-on:click="openAddSidebar"><i class="fas fa-pen-square"></i>Edit</a></li>
				<li><a v-on:click="clickDelete"><i class="fas fa-trash"></i>Delete</a></li>
			</template>
		</ul>
	</aside>
</template>

<script>
	import MenuForm from "./menuForm";
	import anime from 'animejs'

	export default {
		components: {MenuForm},
		name: "menu-sidebar",
		data() {
			return {
				search : ''
			}
		},
		methods : {
			openAddSidebar : function (event) {
				anime({
					targets : '.menu.absolute',
					translateX : this.$el.clientWidth,
					easing: 'easeInOutQuart'
				})
			},
			clickDelete : function() {
				this.$store.dispatch('deleteMovie', Number(this.$route.params.id)).then(() => {
					this.$router.push({ name : 'list'});
				});
			},
			saveSearch : function() {
				console.log("change");
				this.$store.dispatch('saveSearch', this.search);
			}
		}
	}
</script>

<style scoped>

</style>