<script>
export let msg_show;
export let msg_text;
export let msg_type;


import { auth } from 'store/index.js';


import { get } from 'svelte/store';
import { createForm } from 'svelte-forms-lib';
import * as yup from 'yup';
import { navigateTo, Navigate } from 'svelte-router-spa';

import { onMount } from 'svelte';


import FormFieldError from 'components/forms/FormFieldError.svelte';



const api_url = app_.env.API_URL;
// const hcaptcha_site_key = app_.env.HCAPTCHA_SITE_KEY;

let loading = false;



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
		username: '',
		password: '',
	},
	validationSchema: yup.object().shape({
		username: yup
			.string()
			.required('Username required!'),
		password: yup
			.string()
			.required('Password required!'),
	}),
	onSubmit: values => {

		loading = true;

		let form_data = new FormData();

		form_data.append('username', values.username);
		form_data.append('password', values.code);

		submitForm(form_data).then(data => {

			auth.set({token: data.access_token});
			navigateTo('/logged-in');

		}).catch(error => {

			msg_type = 'error';
			msg_show = true;

		}).finally(() => {

			loading = false;

		});
		
	}
});


async function submitForm(form_data) {

	const url = `${api_url}/_auth/access-token`;

	const resp = await fetch(url, {
		method: 'POST',
		body: form_data,
	});

	const result = await resp.json();

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

			<input placeholder="Uername" class="input" type="text" id="username" name="username" on:change={handleChange} bind:value={$form.username}>

			{#if $errors.username}
				<FormFieldError detail={$errors.username} />
			{/if}

		</div>

	</div>

	<div class="field">

		<div class="control">

			<input placeholder="Password" class="input" type="password" id="password" name="password"  on:change={handleChange} bind:value={$form.password}>

			{#if $errors.password}
				<FormFieldError detail={$errors.password} />
			{/if}

		</div>

	</div>


	<div class="field is-grouped">

		<div class="control">

			<button  class="button is-blue">
				<span>Continue</span>
				<i class="fas fa-circle-notch fa-spin" class:is-hidden={!loading}></i>
			</button>

		</div>

	</div>

</form>

