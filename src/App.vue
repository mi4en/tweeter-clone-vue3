<template>
	<div id="app">
		<nav>
			<router-link to="/">
				<div class="navigation__logo">
					Twotter
				</div>
			</router-link>
			<div class="navigation__user" v-if="user">
				{{ user.username }}
			</div>
		</nav>
		<router-view />
	</div>
</template>

<script>
import { useStore } from 'vuex';
import { onMounted, computed } from 'vue';
import { users } from './assets/users';
export default {
	name: 'App',
	setup() {
		onMounted(async () => {
			await store.dispatch('User/setUser', users[0]);
		});

		const store = useStore();

		const user = computed(() => store.state.User.user);
		return {
			user,
		};
	},
};
</script>

<style lang="scss">
nav {
	display: flex;
	align-items: center;
	justify-content: space-between;
	padding: 10px 5%;
	background-color: steelblue;
	color: #fff;
	.navigation__logo {
		font-weight: bold;
		font-size: 24px;
	}
	.navigation__user {
		font-weight: bold;
	}
}
</style>
