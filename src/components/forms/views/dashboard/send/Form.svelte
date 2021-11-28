<script>
export let msg_show;
export let msg_text;
export let msg_type;
// export let balance;


import { auth } from 'store/index.js';


import { get } from 'svelte/store';
import { createForm } from 'svelte-forms-lib';
import * as yup from 'yup';
import { navigateTo, Navigate } from 'svelte-router-spa';

import { onMount } from 'svelte';


import FormFieldError from 'components/forms/FormFieldError.svelte';



const api_url = app_.env.API_URL;

const token = get(auth).token;

// const hcaptcha_site_key = app_.env.HCAPTCHA_SITE_KEY;

let loading = false;


let packet_sent = false;

let link = '';


const {
	form,
	errors,
	state,
	// handleBlur,
	handleChange,
	handleSubmit,
	setField,
} = createForm({
	initialValues: {
		celo_value_amount: '',
		recipients_amount: '',
		message: '',
	},
	validationSchema: yup.object().shape({
		celo_value_amount: yup
			.number()
			.required('Amount'),
		recipients_amount: yup
			.number()
			.required(),
		message: yup
			.string()
			.required(),
	}),
	onSubmit: values => {

		loading = true;

		let body_data = JSON.stringify(values);

		submitForm(body_data).then(data => {

			alert('Packet Sent!');

			packet_sent = true;
			link = data.link;
			// navigateTo!...

		}).catch(error => {

			console.log(error);
			alert('Error!');
			// msg_type = 'error';
			// msg_show = true;

		}).finally(() => {

			loading = false;

		});
		
	}
});


async function submitForm(body_data) {

	const url = `${api_url}/_sender/pockets`;

	const resp = await fetch(url, {
		method: 'POST',
		body: body_data,
		headers: {
			Authorization: `Bearer ${token}`,
			'Content-Type': 'application/json',
		},
	});

	const result = await resp.json();

	console.log(result);

	if (!resp.ok) {
		msg_text = result.detail;
		throw new Error('Error!');
	}

	return result;

}


</script>


<style>

form {

}

</style>


<form on:submit={handleSubmit}>

	<div class="field">

		<div class="control">

			<label>Celo Packet Amount</label>

			<input placeholder="Celo Packet Amount" class="input" type="number" id="celo_value_amount" name="celo_value_amount" on:change={handleChange} bind:value={$form.celo_value_amount}>

			{#if $errors.celo_value_amount}
				<FormFieldError detail={$errors.celo_value_amount} />
			{/if}

		</div>

	</div>

	<div class="field">

		<div class="control">

			<label>Total Recipients</label>

			<input placeholder="Total Recipients" class="input" type="number" id="recipients_amount" name="recipients_amount" on:change={handleChange} bind:value={$form.recipients_amount}>

			{#if $errors.recipients_amount}
				<FormFieldError detail={$errors.recipients_amount} />
			{/if}

		</div>

	</div>


	<div class="field">

		<div class="control">

			<label>Message</label>

			<input placeholder="Message" class="input" type="text" id="message" name="message" on:change={handleChange} bind:value={$form.message}>

			{#if $errors.message}
				<FormFieldError detail={$errors.message} />
			{/if}

		</div>

	</div>

	{#if !packet_sent}

	<div class="field is-grouped">

		<div class="control">

			<button  class="button is-blue">
				<span>Create Packet</span>
				<i class="fas fa-circle-notch fa-spin" class:is-hidden={!loading}></i>
			</button>

		</div>

	</div>

	{:else}

	<div class="field is-grouped">

		<div class="control">

			<div lass="button is-blue">
				<span>Share</span>
			</div>

		</div>

	</div>

	<div class="field is-grouped">

		<div class="control">

			<div lass="button is-blue">
				<span>Copy Link: https://ismach-celo-front-web.vercel.app/dashboard/packet/{link}</span>
			</div>

		</div>

	</div>

	{/if}

</form>

