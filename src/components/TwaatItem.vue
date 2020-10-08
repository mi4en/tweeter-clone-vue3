<template>
	<div class="twaat-item" @click="favouriteTwaat(twaat.id)">
		<div class="user-profile__twaat">
			<div class="twaat-item__user">@{{ username }}</div>
			<div class="twaat-item__content">{{ twaat.content }}</div>
		</div>
	</div>
</template>

<script>
export default {
	name: 'TwaatItem',

	props: {
		username: {
			type: String,
			required: true,
		},
		twaat: {
			type: Object,
			required: true,
		},
	},
	methods: {
		favouriteTwaat(id) {
			this.$emit('favourite', id);
		},
	},
};
</script>

<style scoped>
.twaat-item {
	width: 80%;
	padding: 20px;
	background-color: #fff;
	border: 1px solid #dfe3e8;
	border-radius: 5px;
	cursor: pointer;
	transition: all 0.25s ease;
}

.twaat-item:hover {
	transform: scale(1.1, 1.1);
}

.twaat-item__user {
	font-weight: bold;
}
</style>
