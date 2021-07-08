<script>

import Modal from './Modal.svelte'
import AddPatientForm from './AddPatientForm.svelte'
import FHIR_Patient from "../FHIR_Patient.json";

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

//HUSK! Spørsmålstegn (null-sjekk) fører til feil med dips sin embedded browser
 function setPatientData(data) {	
 	console.log("her:", data);
    let familyName = data.entry[0].resource.name[0].family;
 	let givenName = data.entry[0].resource.name[0].given[0];
 	patientName = givenName + " " + familyName;
 	patientId = data.entry[0].resource.identifier[0].value;
 }

const client = new FHIR.client("http://localhost:8080/fhir");
client.request("Patient").then(data => setPatientData(data));

// const newPatient = {
//         method: "POST",
//         body: JSON.stringify(FHIR_Patient),
//         headers: {"Content-Type": "application/json",}
//     }


//     fetch("http://localhost:8080/fhir/Patient", newPatient).then((res) => res.json())
//     .then((res) => console.log("Added new patient:",res));

// 	fetch("http://localhost:8080/fhir/Patient").then(response => response.json()).then(data => console.log("NEW data:",data.entry));
// 	fetch("http://localhost:8080/fhir/Patient?_elements=gender").then(response => response.json()).then(data => console.log("elments data:",data.entry[0].resource.gender));
	
// 	fetch("http://localhost:8080/fhir/Patient").then(response => response.json()).then(data => setPatientData(data));


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