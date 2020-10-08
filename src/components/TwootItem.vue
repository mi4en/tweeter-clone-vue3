<template>
	<div class="twoot-item" @click="favouritetwoot(twoot.id)">
		<div class="user-profile__twoot">
			<div class="twoot-item__user">@{{ username }}</div>
			<div class="twoot-item__content">{{ twoot.content }}</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'twootItem',

	props: {
		username: {
			type: String,
			required: true,
		},
		twoot: {
			type: Object,
			required: true,
		},
	},
	methods: {
		favouritetwoot(id) {
			this.$emit('favourite', id);
		},
	},
};
</script>

<style scoped>
.twoot-item {
	width: 80%;
	padding: 20px;
	background-color: #fff;
	border: 1px solid #dfe3e8;
	border-radius: 5px;
	cursor: pointer;
	transition: all 0.25s ease;
}

.twoot-item:hover {
	transform: scale(1.1, 1.1);
}

.twoot-item__user {
	font-weight: bold;
}
</style>
