<script>
export let currentRoute;

import Loading from 'components/elements/Loading.svelte';

import { auth } from 'store/index.js';
import { get } from 'svelte/store';


const api_url = app_.env.API_URL;
const token = get(auth).token;


let too_late = false;

async function getPacket() {

	const url = `${api_url}/_dashboard/packets/${currentRoute.namedParams.slug}`;

	const resp = await fetch(url, {
		headers: {
			Authorization: `Bearer ${token}`,
		},
	});

	const result = await resp.json();

	if (!resp.ok) {
		console.log(result);
		throw new Error('...');
	}

	return result;

}



async function collectPayment() {

	const url = `${api_url}/_receiver/collect/${currentRoute.namedParams.slug}`;

	const resp = await fetch(url, {
		headers: {
			Authorization: `Bearer ${token}`,
		},
	});

	const result = await resp.json();

	if (!resp.ok) {
		if (result.detail === 'Not in time!') {
			too_late = true;
		} else if (result.detail === 'Collected payment already!') {
			// alert('...!')
			return;
		} else {
			throw new Error('Error!');
		}
		console.log(result);
	}

	return result;

}


let promise = Promise.all([
	collectPayment(),
	getPacket(),
]);


</script>


<style>

</style>


{#await promise}

<Loading />

{:then data}

<section class="section">

	<div class="container">


		{#if !too_late}

		<div class="field">

			<div class="control">

				<label>You Got a Lucky Packet!</label>

				<input class="input" type="number" readonly value="{data[0].amount}">
				CELO

			</div>

		</div>

		{:else}

		<p class="text has-text-centered">
			No more lucky packets!
		</p>

		{/if}


		<br>

		<p class="text has-text-centered">
			Leaderboard
		</p>

		<!-- {data[0].txns} -->

		{#each data[1].txns as txn}

			<p class="text has-text-centered">{txn}</p><br><br>

			<!-- {#if !!txn.values()[0]}
				{txn.values()[0]}
			{/if} -->

		{/each}


		<!-- Leaderboard! -->

	</div>

</section>

{:catch error}

error.

{/await}

