<script lang="ts">
	import { supabaseClient } from '$lib/supabaseClient';

	let loading = false;
	let email: string;
	let password: string;

	const handleLogin = async () => {
		try {
			loading = true;
			const { data, error } = await supabaseClient.auth.signUp({ email, password });

			console.log(data, error);
			if (error) throw error;
			alert('Check your email for the login link!');
		} catch (error) {
			if (error instanceof Error) {
				alert(error.message);
			}
		} finally {
			loading = false;
		}
	};
</script>

<form class="row flex-center flex" on:submit|preventDefault={handleLogin}>
	<div class="col-6 form-widget">
		<h1 class="header">Supabase + SvelteKit</h1>

		<div>
			<input class="" type="email" placeholder="Your email" bind:value={email} />
			<input class="" type="password" placeholder="Password" bind:value={password} />
		</div>

		<div>
			<input
				type="submit"
				class="button block"
				value={loading ? 'Loading' : 'Send magic link'}
				disabled={loading}
			/>
		</div>
	</div>
</form>
