<script>
  import { oauth2 as Smart } from "fhirclient";
  import { onMount } from "svelte";

  //onMount(async () => {
  Smart.authorize({
    clientId: "sykepenger_dokument",
    scope:
      "launch openid fhirUser patient/*.read patient/*.write offline_access documentReference/*.read documentReference/*.write",
    patientId: "123",
    redirectUri: "./app",
    iss: "https://foi.dips.fhir.service.sandbox.dips.no",
    launch:
      "6c5d9ca9-54d7-42f5-bfae-a7c19cd217f2::DocumentReference/b3e32146-848c-4d3b-b8a9-c9b3a7861a6a",
  });
  //});
</script>

<!-- <script>
  import { oauth2 as Smart } from "fhirclient";
  import { onMount } from "svelte";

  onMount(async () => {
    Smart.authorize({
      clientId: "sykepenger_dokument",
      scope:
        "launch openid fhirUser patient/*.read patient/*.write offline_access documentReference/*.read documentReference/*.write",
      //launch: "https://localhost:9000",
      patientId: "123",
      redirectUri: "./code",
      //iss:'https://vt-selecta-b.dips.local/DIPS-WebAPI/HL7/FHIR-R4',
      iss: "https://foi.dips.fhir.service.sandbox.dips.no",
      launch:
        "6c5d9ca9-54d7-42f5-bfae-a7c19cd217f2::DocumentReference/b3e32146-848c-4d3b-b8a9-c9b3a7861a6a",
    });
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
</script> -->
