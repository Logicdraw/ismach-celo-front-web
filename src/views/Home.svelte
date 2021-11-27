<script>
import { Navigate } from 'svelte-router-spa';


</script>


<style>

.hero {
	background-color: #000;
}

</style>


<section class="hero is-fullheight">

	<div class="hero-body">

		<div class="container" style="max-width: 960px;">

			<p class="hero-title has-text-centered">
				Celo <span style="">Gold</span> Packet
			</p>

			<p class="hero-subtitle has-text-centered">
				Send random gifts  to friends and see who is <span style="">the luckiest of them all!</span>
			</p>

			
			<img src="" style="">


			<Navigate styles="button is-white" to='/login?next_link=/dashboard/send'>
				Send Now
			</Navigate>


		</div>

	</div>

</section>



