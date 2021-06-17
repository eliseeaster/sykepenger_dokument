<script>

import Modal from './Modal.svelte'
import AddPatientForm from './AddPatientForm.svelte'
let showModal = false;
let showForm = false;


// Modal
const toggleModal = () => {
	showModal = !showModal;
}

// Form
const ToggleForm = () => {
		showForm = !showForm;
	}

</script>

<Modal header="Information" message="Here is some information" isInfo={true} {showModal} on:click={toggleModal}/>
<main>
	<button on:click={toggleModal}>Open modal</button>
	<button on:click={ToggleForm}>Add new patient</button>
	<AddPatientForm {showForm}/>


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