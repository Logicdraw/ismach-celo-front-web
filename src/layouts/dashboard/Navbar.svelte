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


#dashboard-navbar {

}

</style>



<nav class="navbar is-fixed-top" id="dashboard-navbar">

	<div class="container">


		<div class="navbar-brand">

			<Navigate to="/my/teams" styles="navbar-item" on:click={closeActive}>
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

				<Navigate styles="navbar-item" to="/my/teams" on:click={closeActive}>
					<span on:click={closeActive}>My Teams</span>
				</Navigate>

				<Navigate styles="navbar-item" to="/my/programs" on:click={closeActive}>
					<span on:click={closeActive}>My Programs</span>
				</Navigate>

				<Navigate styles="navbar-item" to="/my/camps" on:click={closeActive}>
					<span on:click={closeActive}>My Camps</span>
				</Navigate>

				<Navigate styles="navbar-item" to="/my/free-agents" on:click={closeActive}>
					<span on:click={closeActive}>Free Agents</span>
				</Navigate>

				<div class="navbar-item has-dropdown is-hoverable" style="z-index: 100;">

					<a class="navbar-link">
						<span>Corner</span>
					</a>

					<div class="navbar-dropdown" style="z-index: 10001;">

						<Navigate styles="navbar-item" to="/my/coaches-corner/resources" on:click={closeActive}>
							<span on:click={closeActive}>Resources</span>
						</Navigate>

						<Navigate styles="navbar-item" to="/my/coaches-corner/messages" on:click={closeActive}>
							<span on:click={closeActive}>Messages</span>
						</Navigate>

					</div>


				</div>

			</div>


			<div class="navbar-end">

				<div class="navbar-item has-dropdown is-hoverable" style="z-index: 100;">


					<a class="navbar-link">
						<span>More</span>
					</a>

					<div class="navbar-dropdown is-right" style="z-index: 10001;">

						<Navigate styles="navbar-item" to="/my/help" on:click={closeActive}>
							<span on:click={closeActive}>Help</span>
						</Navigate>

						<Navigate styles="navbar-item" to="/my/faq" on:click={closeActive}>
							<span on:click={closeActive}>FAQ</span>
						</Navigate>

					</div>


				</div>


				<Navigate styles="navbar-item" to="/logout" on:click={closeActive}>
					<span on:click={closeActive}>Logout</span>
				</Navigate>


			</div>


		</div>


	</div>

</nav>


