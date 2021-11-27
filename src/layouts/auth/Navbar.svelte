<script>
import { Navigate } from 'svelte-router-spa';


let active = false;


function changeActive() {
	active = !active;
}

function closeActive() {
	active = false;
}

</script>



<style>


#auth-navbar {

}

</style>



<nav class="navbar is-fixed-top" id="auth-navbar">

	<div class="container">


		<div class="navbar-brand">

			<Navigate to="/login" styles="navbar-item" on:click={closeActive}>
				<img src="/img/logo.png" style="width: 37px !important;">
				<span>AHG Coaches</span>
			</Navigate>

			<a role="button" class="navbar-burger burger" aria-label="menu" aria-expanded="false" data-target="navbar-items" on:click={changeActive} class:is-active={active}>
				<span aria-hidden="true"></span>
				<span aria-hidden="true"></span>
				<span aria-hidden="true"></span>
			</a>

		</div>


		<div class="navbar-menu" id="navbar-items" class:is-active={active}>


			<div class="navbar-start">

			</div>


			<div class="navbar-end">

				<Navigate styles="navbar-item" to="/contact" on:click={closeActive}>
					<span on:click={closeActive}>Contact</span>
				</Navigate>

				<Navigate styles="navbar-item" to="/login" on:click={closeActive}>
					<span on:click={closeActive}>Login</span>
				</Navigate>

			</div>


		</div>


	</div>

</nav>


