<script>
  import { Router, Route } from "svelte-routing";
  import Launch from "./Launch.svelte";
  import Code from "./Code.svelte";
  import Test from "./Test.svelte";

  export let url = "";
</script>

<Router {url}>
  <Route path="/">
    <Launch />
  </Route>
  <Route path="/app">
    <Code />
  </Route>
  <Route path="/test">
    <Test />
  </Route>
</Router>
