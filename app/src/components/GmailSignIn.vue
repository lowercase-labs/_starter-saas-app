<template>
	<div class="mt-6">
		<div>
			<button
				@click="onGmailClick"
				class="w-full inline-flex justify-center py-2 px-4 border border-gray-300 rounded-md shadow-sm bg-white text-sm font-medium text-gray-500 hover:bg-gray-50 focus:outline-none"
			>
				<span class="sr-only">Sign in with Gmail</span>
				<svg
					width="24px"
					version="1.1"
					id="Layer_1"
					xmlns="http://www.w3.org/2000/svg"
					xmlns:xlink="http://www.w3.org/1999/xlink"
					viewBox="0 0 512 512"
					xml:space="preserve"
				>
					<g>
						<polygon
							style="fill:#F2F2F2;"
							points="484.973,122.808 452.288,451.017 59.712,451.017 33.379,129.16 256,253.802 	"
						/>
						<polygon
							style="fill:#F2F2F2;"
							points="473.886,60.983 256,265.659 38.114,60.983 256,60.983 	"
						/>
					</g>
					<path
						style="fill:#F14336;"
						d="M59.712,155.493v295.524H24.139C10.812,451.017,0,440.206,0,426.878V111.967l39,1.063L59.712,155.493z"
					/>
					<path
						style="fill:#D32E2A;"
						d="M512,111.967v314.912c0,13.327-10.812,24.139-24.152,24.139h-35.56V155.493l19.692-46.525L512,111.967z"
					/>
					<path
						style="fill:#F14336;"
						d="M512,85.122v26.845l-59.712,43.526L256,298.561L59.712,155.493L0,111.967V85.122c0-13.327,10.812-24.139,24.139-24.139h13.975L256,219.792L473.886,60.983h13.962C501.188,60.983,512,71.794,512,85.122z"
					/>
					<polygon style="fill:#D32E2A;" points="59.712,155.493 0,146.235 0,111.967 " />
				</svg>
			</button>
		</div>
	</div>
</template>

<script>
	export default {
		methods: {
			onGmailClick() {
				this.$store.dispatch("auth/signInGoogle");
			},
		},
	};
</script>

<style>
</style>
