<script>
export let currentRoute;


import Loading from 'components/elements/Loading.svelte';


import { Navigate } from 'svelte-router-spa';


import { auth } from 'store/index.js';


import { get } from 'svelte/store';
import SvelteSeo from 'svelte-seo';



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
		throw new Error(result.detail);
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

		<div class="field">

			<div class="control">

				<label>Balance</label>

				<input class="input" disabled value="{data[0].balance} CELO">

			</div>

		</div>

		<div class="field">

			<div class="control">

				<Navigate styles='' to='/dashboard/send'>
					Send a Gold Packet
				</Navigate>

			</div>

		</div>

		<div class="field">

			<div class="control">

				<button class="button">
					Deposit
				</button>

			</div>

		</div>

		<div class="field">

			<div class="control">

				<button class="button">
					Withdraw
				</button>

			</div>

		</div>


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

error

{/await}

