<script>

import Modal from './Modal.svelte'
import AddPatientForm from './AddPatientForm.svelte'

let showModal = false;
let patientName;
let patientId;
let comment;
let readonly;

// Modal
const toggleModal = () => {
	showModal = !showModal;
}

const urlParams = new URLSearchParams(window.location.search);
patientId = urlParams.get("id");
patientName = urlParams.get("name");
readonly = urlParams.get("readonly");

if(readonly == "true") {
	readonly = true;
}else{
	readonly = false;
}

//Console log every parameter in url
urlParams.forEach(
	param => console.log(param)
)

</script>
	<main>
		<div class:disable={readonly}>
			<Modal header="Information" message="Here is some information" isInfo={true} {showModal} on:click={toggleModal}/>
			<button on:click={toggleModal}>?</button>
			<AddPatientForm  bind:patientName bind:patientId bind:readonly/>
		</div>
	</main>

<style>

	main{
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	.disable{
		pointer-events: none;
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