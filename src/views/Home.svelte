<script>
export let currentRoute;


import { Navigate } from 'svelte-router-spa';


// import ModalValora from 'components/elements/ModalValora.svelte';


</script>


<style>

.hero {
	background-color: #000;
}

.hero-title {
	/*color: #fff;*/
}

.hero-subtitle {
	font-size: 1.75rem;
	color: #fff;
	margin-bottom: 1rem;
}


:global(.button.is-centered) {
	display: block;
	width: fit-content;
	margin: 0 auto;
	font-weight: 500;
	font-size: 1.125rem;
	color: #000;
	border-radius: 1.25em;
}

</style>


<!-- <ModalValora is_active={true} /> -->


<section class="hero is-fullheight">

	<div class="hero-body">

		<div class="container" style="max-width: 960px;">

			<p class="hero-title has-text-centered">
				Celo <span style="color: gold;">Gold</span> Packet
			</p>

			<p class="hero-subtitle has-text-centered">
				Send random gifts  to friends and see who is <span style="color: #21b921;">the luckiest of them all!</span>
			</p>

			
			<img src="" style="display: block;">

			<br>

			<Navigate styles="button is-white is-centered" to='/login?next_link=/dashboard/home'>
				Send Now
			</Navigate>


		</div>

	</div>

</section>




