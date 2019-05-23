<script>
		import { onMount } from "svelte";
		import CopyLink from "./CopyLink.svelte";
		import axios from "axios";
		let count = 0;
		let excuses = [];
		axios
		  .get("https://us-central1-wfh-excuses-gh.cloudfunctions.net/wfh", {
		    headers: { "Access-Control-Allow-Origin": "*" }
		  })
		  .then(function(response) {
		    // handle success
		    console.log(response);
		  })
		  .catch(function(error) {
		    // handle error
		    console.log(error);
		  })
		  .finally(function() {
		    // always executed
		  });

		let excuse = "";

		function handleClick() {
		  excuse = excuses[Math.floor(Math.random() * excuses.length)];
		}

		onMount(() => {
		  excuse = excuses[Math.floor(Math.random() * excuses.length)];
		});
</script>

<style>
	.msg_container:before {
	  width: 0;
	  height: 0;
	  top: -5px;
	  left: -14px;
	  position: relative;
	  border-style: solid;
	  border-width: 0 13px 13px 0;
	  border-color: transparent #ffffff transparent transparent;
	}
	.msg_container {
	  font-family: "Lobster", cursive;
	  font-size: 35px;
	  margin-top: auto;
	  margin-bottom: auto;
	  margin-left: 10px;
	  border-radius: 25px;
	  background-color: #4ac8e4;
	  padding: 25px;
	  position: relative;
	}
</style>

<div class="d-flex justify-content-center mb-5">
	<div class="msg_container">
		<strong>{excuse}</strong>
	</div>
	<CopyLink/>	
</div>

<button on:click={handleClick} class="btn btn-primary">
  Generate New Excuse
</button>