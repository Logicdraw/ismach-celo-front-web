<script>
export let currentRoute;

import Form from 'components/forms/views/auth/login/Form.svelte';


let next_link = currentRoute.queryParams;


</script>


<style>

</style>


<section class="section">

	<div class="container">

		<div class="columns is-centered">

			<div class="column is-8-desktop is-10-tablet is-12-mobile">

				<Form {next_link} />

			</div>

		</div>

	</div>

</section>



