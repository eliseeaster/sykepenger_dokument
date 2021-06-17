

<script>

 import { dataset_dev, text } from "svelte/internal";
import Modal from './Modal.svelte'
let showModal = true;

const toggleModal = () => {
	showModal = !showModal;
}

	export let name;
	let dips_bilde = "dips.png"

	let patients = [
		{Name: "Åge", Age: 24, Gender: "Male", id: 0},
		{Name: "Sara", Age: 29, Gender: "Female", id: 1}
	]

	let patientName;
	let age;
	let gender = 0;


	let showForm = false;

	const ToggleForm = () => {
		showForm = !showForm;
	}

	const addPatient = () => {
		let g = "Male";
		{if (gender==1) {
			g = "Female";
		}}
		
		let newPatient = {Name: patientName, Age: age, Gender: g, id: patients.length};
		patients[patients.length] = newPatient; 
		console.log(newPatient);
		showForm = false;
		resetFields();
	}

	const resetFields = () => {
		patientName = "";
		age = "";
		gender = 0;
	}

</script>

<Modal header="Information" message="Here is some information" isInfo={true} {showModal} on:click={toggleModal}/>
<main>
	<button on:click={toggleModal}>Open modal</button>

	<img src="favicon.png" alt="svelte logo"/>
	<img src={dips_bilde} alt="dipsbilde"/>
	<h1>Hello {name}!</h1>
	<p>Visit the <a href="https://svelte.dev/tutorial">Svelte tutorial</a> to learn how to build Svelte apps.</p>

	<h2>Patient List</h2>
	{#each patients as patient (patient.id)}
		<div>
			<h3>{patient.Name}</h3>
		</div>
	{/each}
	
	{#if showForm === false}
		<button on:click = {ToggleForm}>Add new patient</button>
	{:else}
		<form on:submit|preventDefault={addPatient}>
			<input type= "text" placeholder="Name" bind:value={patientName} required/>
			<input type= "number" placeholder="Age" bind:value={age} required/>
			<label>
				<input type= "radio" bind:group={gender} value={0} required/>
				Male
			</label>
			<label>
				<input type= "radio" bind:group={gender} value={1} required/>
				Female
			</label>
			<button>Add patient</button>
		</form>
		
	{/if}
	
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