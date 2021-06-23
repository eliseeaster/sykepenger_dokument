<script>

import Modal from './Modal.svelte'
import AddPatientForm from './AddPatientForm.svelte'
import { get } from 'svelte/store';
let showModal = false;
// let showForm = false;

let patientName = "Andreas";
let patientId = "55555";

	window.chrome.webview.addEventListener('message', event => alertSomething(event.data));

// Modal
const toggleModal = () => {
	showModal = !showModal;
}

const alertSomething = (e) => {
	console.log(e);
	if(e == "heihei"){
		alert(e);
		saveDoc();
	}else if(e == "Elise"){
		patientName = e;
		console.log(patientName)
		alert(e)
	}
	else {
		alert("Not saving");
	}
	
}

const saveDoc = () => {
	alert("saving document");
	//window.chrome.webview.postMessage("Melding fra svelte-app");
}

// function alertSomething(){
// 	alert("elise");
// }

//window.addEventListener('load', alertSomething);




</script>

<Modal header="Information" message="Here is some information" isInfo={true} {showModal} on:click={toggleModal}/>
<main>
	<button on:click={toggleModal}>?</button>
	<div>
		<label>Navn</label>
		<input disabled bind:value={patientName}/>
		<label>Personnummer</label>
		<input disabled value={patientId}/>
		
	</div>
	
	<!-- <button on:click={ToggleForm}>Lag ny</button> -->
	<AddPatientForm  bind:patientName bind:patientId/>

</main>

<style>

	main{
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	h1 {
		color: red;
		text-transform: uppercase;
		font-size: 4em;
		font-weight: 100;
	}

	@media (min-width: 640px) {
		main {
			max-width: none;
		}
	}

</style>