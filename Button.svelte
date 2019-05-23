<script>
	import { onMount } from "svelte";
	import CopyLink from "./CopyLink.svelte";
	let count = 0;
	let excuses = [
	  "Got cramps, can't really do anything right now..",
	  "My doctor told me I should rest at home.",
	  "I need to do something in a few minutes, sorry."
	];
	let excuse = "";

	function handleClick() {
	  excuse = excuses[Math.floor(Math.random() * excuses.length)];
	}

	onMount(() => {
	  excuse = excuses[Math.floor(Math.random() * excuses.length)];
	});
</script>

<style>
	.msg_cotainer:before {
	  width: 0;
	  height: 0;
	  top: -5px;
	  left: -14px;
	  position: relative;
	  border-style: solid;
	  border-width: 0 13px 13px 0;
	  border-color: transparent #ffffff transparent transparent;
	}
	.msg_cotainer {
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
	<div class="msg_cotainer">
		<strong>{excuse}</strong>
	</div>
	<CopyLink/>
</div>

<button on:click={handleClick} class="btn btn-primary">
  Generate New Excuse
</button>