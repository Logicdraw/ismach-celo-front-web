<script>
export let currentRoute;


import Loading from 'components/elements/Loading.svelte';

import { auth } from 'store/index.js';
import { get } from 'svelte/store';


import SendForm from 'components/forms/views/dashboard/send/Form.svelte';


const api_url = app_.env.API_URL;
const token = get(auth).token;


async function getBalance() {

	const url = `${api_url}/_dashboard/balance`;

	const resp = await fetch(url, {
		headers: {
			Authorization: `Bearer ${token}`,
		},
	});

	const result = await resp.json();

	if (!resp.ok) {
		throw new Error('Error!');
	}

	return result;

}

let promise = Promise.all([
	getBalance(),
]);


</script>


<style>

</style>


{#await promise}

<Loading />

{:then data}

<section class="section">

	<div class="container">

		<SendForm />


		<div class="field">

			<div class="control">

				<a href="#">
					Account Settings
				</a>

			</div>

		</div>

	</div>

</section>

{:catch error}

error.

{/await}

