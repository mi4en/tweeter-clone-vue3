<template>
	<div class="user-profile">
		<div class="user-profile__user-panel">
			<h1 class="user-profile__username">@{{ user.username }}</h1>

			<div v-if="user.isAdmin" class="user-profile__admin-badge">Admin</div>

			<div class="user-followers-count"><strong>Followers: </strong> {{ followers }}</div>

			<form class="user-profile__create-twaat" @submit.prevent="createNewTwaat">
				<label for="newTwaat"><strong>New Twaat</strong></label>
				<textarea id="newTwaat" rows="4" v-model="newTwaatContent"></textarea>

				<div class="user-profile__create-twaat-type">
					<label for="newTwaatType"><strong>Type: </strong></label>
					<select id="newTwaatType" v-model="selectedTwaatType">
						<option :value="option.value" v-for="(option, index) in twaatTypes" :key="index">
							{{ option.name }}
						</option>
					</select>
				</div>

				<button>
					Twaat!
				</button>
			</form>
		</div>

		<div class="user-profile__twaats-wrapper">
			<TwaatItem
				class="user-profile__twaat"
				v-for="twaat in user.twaats"
				:key="twaat.id"
				:username="user.username"
				:twaat="twaat"
				@favourite="toggleFavourite"
			/>
		</div>
	</div>
</template>

<script>
import TwaatItem from '../components/TwaatItem';

export default {
	name: 'UserProfile',
	components: {
		TwaatItem,
	},

	data: () => ({
		newTwaatContent: '',
		selectedTwaatType: 'instant',
		followers: 0,
		user: {
			id: 1,
			username: 'subZero',
			firstName: 'Sub',
			lastName: 'Zero',
			email: 'subzero@mk.com',
			isAdmin: true,
			twaats: [
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
		twaatTypes: [
			{
				value: 'draft',
				name: 'Draft',
			},
			{
				value: 'instant',
				name: 'Instant Twaat',
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
			console.log(`New favourite twaat with id ${id}`);
		},
		createNewTwaat() {
			if (this.newTwaatContent && this.selectedTwaatType !== 'draft') {
				this.user.twaats.unshift({
					id: this.user.twaats.length + 1,
					content: this.newTwaatContent,
				});

				this.newTwaatContent = '';
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

.user-profile__twaats-wrapper {
	display: grid;
	gap: 10px;
}

.user-profile__create-twaat {
	display: flex;
	flex-direction: column;
	padding-top: 20px;
}
</style>
