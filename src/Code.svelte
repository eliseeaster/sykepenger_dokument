<script>

    import Modal from './Modal.svelte'
    import AddPatientForm from './AddPatientForm.svelte'
    import FHIR_Patient from "../FHIR_Patient.json";
    import {oauth2 as Smart} from 'fhirclient';
    import {onMount} from 'svelte';
    import { derived, writable } from 'svelte/store';
    import {resource} from './SmartOnFhirStore';
    
    
    let showModal = false;
    let patientName;
    let patientId;
    let comment;
    let readonly;
    let address;
    
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
        let familyName = data.name[0].family;
         let givenName = data.name[0].given[0];
         patientName = givenName + " " + familyName;
         patientId = data.identifier[0].value;
        address = data.address[0].line[0];
     }
    
    const client = new FHIR.client("http://localhost:8080/fhir/");
    client.request("Patient/3458").then(data => setPatientData(data));
    
    // const h = new AuthTicket("auth-tiket");
    // const k = new authTicketCode("fad3f55a-b3a3-455f-80b0-bd4f82c29bf6");
    
    // const socket = new WebSocket("ws://vt-selecta-b.dips.local/DIPS-WebAPI/HL7/FHIR-R4/", "auth-tiket", "fad3f55a-b3a3-455f-80b0-bd4f82c29bf6");
    // socket.request("Patient/13116900216").then(data => console.log(data));
    // socket.send()
    
    // const newClient = {
    // 	url: "https://vt-selecta-b.dips.local/DIPS-WebAPI/HL7/FHIR-R4/",
        
    // }
    
    
    //const client2 = new FHIR.client("https://vt-selecta-b.dips.local/DIPS-WebAPI/HL7/FHIR-R4/");
    
    
  
    //	fhir.client.patient.read().then(console.log);
    // client2.oauth2.( {
    // 	client_id: 'fad3f55a-b3a3-455f-80b0-bd4f82c29bf6',
    // 	scope: 'launch launch/patient patient/DocumentReference.write patient/DocumentReference.read patient/Patient.read patient/encounter patient/resource online_access openid fhirUser'
    // });
    
    // const auth = {
    // 			method: "GET",
    // 			headers: {"auth-ticket" : "fad3f55a-b3a3-455f-80b0-bd4f82c29bf6"},
    // 			url: "Patient/identifier=13116900216"
                
    // 		}
    
    // let AuthTicket = "auth-ticket";
    // let authTicketCode = "fad3f55a-b3a3-455f-80b0-bd4f82c29bf6";
    
    // const client2 = new FHIR.client("https://vt-selecta-b.dips.local/DIPS-WebAPI/HL7/FHIR-R4/");
    // client2.Smart.authorize
    
    // client2.request("Patient?identifier=13116900216").then(data => console.log(data));
    
    export function updatePatient2() {
        patientName = "kari";
        alert("hei");
    }
    
    //Comment is saved as the patient's address in the api
    function updatePatient() {
        const newPatient = {
                method: "PUT",
                body: FHIR_Patient,
                headers: {"Content-Type": "application/json",},
                url: "Patient/3458"
            }
        
        newPatient.body.address[0].line[0] = address;
        console.log(newPatient.body);
        newPatient.body = JSON.stringify(newPatient.body);
        
        client.request(newPatient);	
    }
    
    // public class HardCodedAuthorizationMessageHandler : HttpClientHandler
    //     {
    //         string AuthTicket { get; set; }
    //        string authTicketCode { get; set; }
    //         protected async override Task<HttpResponseMessage> SendAsync(HttpRequestMessage request, CancellationToken cancellationToken)
    //         {
    //             request.Headers.Add(AuthTicket, authTicketCode);
    
    //             return await base.SendAsync(request, cancellationToken);
    //         }
    //     }
    
    </script>

        {#if $resource}       
            Found resource
        {:else}
            Loading PDF Document...
        {/if}

        <main>
            <div class:disable={readonly}>
                <Modal header="Information" message="Here is some information" isInfo={true} {showModal} on:click={toggleModal}/>
                <button on:click={toggleModal}>?</button>
                <AddPatientForm  bind:patientName bind:patientId bind:readonly bind:address/>
                <button id="SaveDocument" on:click={updatePatient}>Trykk her</button>
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
    
        .hide button {
            display: none;
        }
    
    </style>