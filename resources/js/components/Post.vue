<template>
	<div class="my-card position-relative mb-5">
		<div
		class="my-card-img text-center p-2 mx-auto"
		@mouseover="showContent()"
		@mouseleave="hideContent()"
		>
			<img :src="post.image_url" class="img-fluid" :alt="`${post.title} post image`">
		</div>
		<div v-if="isMouseOver" class="my-card-content position-absolute text-white">
			<h5 class="card-title">{{ firstUppercase(post.title) }}</h5>
			<p class="card-text">
				{{post.description}}
			</p>
			<p class="card-text">
				Created on: {{ getDateFormat(post.created_at) }}
			</p>
		</div>
	</div>
</template>

<script>


export default {
	name: 'Post',
	data() {
		return {
			isMouseOver: false,
		}
	},
	props: ['post'],
	methods: {

		getDateFormat(date) {
		const datestring = new Date(date);
		const formattedDate = datestring.getDate()  + "-" + (datestring.getMonth()+1) + "-" + datestring.getFullYear();
		return formattedDate;
		},

		firstUppercase(string) {
		return string.charAt(0).toUpperCase() + string.slice(1);
		},

		showContent() {
			return this.isMouseOver = true;
		},

		hideContent() {
			return this.isMouseOver = false;
		}

	}
}
</script>

<style lang="scss" scoped>

div.my-card {
	.my-card-img {
		width: 80%;
		img {
			-webkit-transition : -webkit-filter 700ms ease-in-out;
			transition: filter 700ms ease-in-out;
			border-radius: 50%;
			filter: blur(0px) brightness(100%);
			&:hover {
				filter: blur(5px) brightness(35%);
			}
		}
	}
	.my-card-content {
		top: 50%;
		left: 50%;
		font-weight: bold;
		transform: translate(-50%, -50%);
		p {
			font-style: italic;
		}
	}
}


</style>