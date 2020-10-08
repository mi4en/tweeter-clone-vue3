<template>
	<div class="user-profile">
		<div class="user-profile__user-panel">
			<h1 class="user-profile__username">@{{ user.username }}</h1>

			<div v-if="user.isAdmin" class="user-profile__admin-badge">Admin</div>

			<div class="user-followers-count"><strong>Followers: </strong> {{ followers }}</div>
		</div>

		<div class="user-profile__twoots-wrapper">
			<TwootItem
				class="user-profile__twoot"
				v-for="twoot in user.twoots"
				:key="twoot.id"
				:username="user.username"
				:twoot="twoot"
				@favourite="toggleFavourite"
			/>
		</div>
	</div>
</template>

<script>
import TwootItem from '../components/TwootItem';
import CreateTwootPanel from '../components/CreateTwootPanel';

export default {
	name: 'UserProfile',
	components: {
		twootItem,
	},

	data: () => ({
		newtwootContent: '',
		selectedtwootType: 'instant',
		followers: 0,
		user: {
			id: 1,
			username: 'subZero',
			firstName: 'Sub',
			lastName: 'Zero',
			email: 'subzero@mk.com',
			isAdmin: true,
			twoots: [
				{
					id: 1,
					content: 'Mortal Kombat',
				},
				{
					id: 2,
					content: 'Shao Kahn suck ballz',
				},
			],
		},
		twootTypes: [
			{
				value: 'draft',
				name: 'Draft',
			},
			{
				value: 'instant',
				name: 'Instant twoot',
			},
		],
	}),
	computed: {
		fullName() {
			return `${this.user.firstName} ${this.user.lastName}`;
		},
	},
	watch: {
		followers(newFolloweCount, oldFollowerCount) {
			if (oldFollowerCount < newFolloweCount) {
				console.log(`${this.user.username} has gained a follower!`);
			}
		},
	},
	methods: {
		followUser() {
			this.followers++;
		},
		toggleFavourite(id) {
			console.log(`New favourite twoot with id ${id}`);
		},
		createNewtwoot() {
			if (this.newtwootContent && this.selectedtwootType !== 'draft') {
				this.user.twoots.unshift({
					id: this.user.twoots.length + 1,
					content: this.newtwootContent,
				});

				this.newtwootContent = '';
			}
		},
	},
	mounted() {
		this.followUser();
	},
};
</script>

<style scoped>
.user-profile {
	display: grid;
	grid-template-columns: 1fr 3fr;
	width: 100%;
	padding: 50px 5%;
}

.user-profile__user-panel {
	display: flex;
	flex-direction: column;
	margin-right: 50px;
	padding: 20px;
	background-color: #fff;
	border: 1px solid #dfe3e8;
	border-radius: 5px;
}

.user-profile__admin-badge {
	background: rebeccapurple;
	color: #fff;
	border-radius: 5px;
	margin-right: auto;
	padding: 0 10px;
	font-weight: bold;
}

h1 {
	margin: 0;
}

.user-profile__twoots-wrapper {
	display: grid;
	gap: 10px;
}

.user-profile__create-twoot {
	display: flex;
	flex-direction: column;
	padding-top: 20px;
}
</style>
