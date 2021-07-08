<script>
	export let patientName;
	export let patientId;
	export let comment = "";
	export let readonly;
	export let dirtyDocument = false;

	const saveDocument = () => {
		dirtyDocument = false;
	};

	const approveDocument = () => {
		dirtyDocument = false;
	};

	const keyPress = () => {

		dirtyDocument = true;
		//window.chrome.webview.postMessage("DocumentStatus:true");
		CefSharp.PostMessage("DocumentStatus:dirty");		
	}

	const emptyDocument = () => {		
		CefSharp.PostMessage("DocumentStatus:empty");		
	}

</script>

<main>
	<div class:hide={readonly}>
		<label>Navn</label>
		<input disabled value={patientName} id="name" />
		<label>Personnummer</label>
		<input disabled value={patientId} id="patientId" />

		<input type="text" placeholder="Kommentar" id="commentBox" value="{comment}" on:input={keyPress} on: on:emptied="{emptyDocument}"/>
		<button
			class:inactive={!dirtyDocument}
			name="saveButton"
			type="submit"
			on:click={saveDocument}
			id="button1">Lagre</button>
		<button name="approveButton" type="submit" on:click={approveDocument} class:inactive={!dirtyDocument}>Godkjenn</button>
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

	.inactive {
		opacity: 0.5;
	}
</style>
