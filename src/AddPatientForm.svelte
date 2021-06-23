<script>

	export let patientName;
	export let patientId;
	let code;
	let comment;

	const saveDocument = () => {
		let document = {Name: patientName, PatientId: patientId, Comment: comment};
		let documentString = JSON.stringify(document)
		console.log(documentString);
		//window.chrome.webview.postMessage()
		window.chrome.webview.postMessage(documentString);
	}

	const approveDocument = () => {
		let document = {Name: patientName, PatientId: patientId, Comment: comment};
		let documentString = JSON.stringify(document)
		console.log("Approved:" + documentString);
	}

</script>

<main>
	
		<!-- <form on:submit|preventDefault={addPatient}> -->
			<!-- <input type= "number" placeholder="Sykemelding kode" bind:value={code} required/> -->

				<input type= "text" placeholder="Kommentar" bind:value={comment} required/>

				<button name="saveButton" type="submit" on:click={saveDocument}>Lagre</button>
				<button name="approveButton" type="submit" on:click={approveDocument}>Godkjenn</button>

			
		<!-- </form> -->
	
</main>

<style>
    
</style>