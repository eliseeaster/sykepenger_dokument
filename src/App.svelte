<script>
	import Launch from "./Launch.svelte";
	import Code from './Code.svelte'
	import {Router, Route} from 'svelte-routing';


</script>

<Router url="">
	<Route path="/">
		<Launch/>
	</Route>
	<Route path="/code">
		<Code/>
	</Route>
</Router>
