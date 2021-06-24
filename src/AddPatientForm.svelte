<script>
	export let patientName;
	export let patientId;
	export let readonly;

	const saveDocument = () => {
		alert("trying to save")
	};

	const approveDocument = () => {
		alert("trying to approve")
	};
</script>

<main>
	<div class:hide={readonly}>
		<label>Navn</label>
		<input disabled value={patientName} id="name" />
		<label>Personnummer</label>
		<input disabled value={patientId} id="patientId" />

		<input type="text" placeholder="Kommentar" id="commentBox"/>
		<button
			name="saveButton"
			type="submit"
			on:click={saveDocument}
			id="button1">Lagre</button
		>
		<button name="approveButton" type="submit" on:click={approveDocument}
			>Godkjenn</button
		>
	</div>
</main>

<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	.hide button {
		display: none;
	}
</style>
