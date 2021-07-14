<script>
    import {oauth2 as Smart} from 'fhirclient';
	import {onMount} from 'svelte';


    Smart.authorize({
			clientId: 'sykepenger_dokument',
			scope: 'launch openid fhirUser patient/*.read patient/*.write offline_access',
            launch:	'https://localhost:9000',			
			redirectUri: '/code',			
            iss:'https://vt-selecta-b.dips.local/DIPS-WebAPI/HL7/FHIR-R4',
			
	
		});


// onMount(async () => {
// 	console.log("mounter")
// 		Smart.authorize({
// 			clientId: 'sykepenger_dokument',
// 			scope: 'launch openid fhirUser patient/*.read patient/*.write offline_access',
//             //launch:	'https://localhost:9000',			
// 			redirectUri: 'https://localhost:9000',			
//             iss:'https://vt-selecta-b.dips.local/DIPS-WebAPI/HL7/FHIR-R4',
			
	
// 		});
// });



</script>  