<script>
	let store_icecreams = ["Vanilla", "Chocochip", "Mint Cookie", "Mango", "Caramel Salted"];
	let store_scoops = [2,5,8,9];
	let icecream = [];
	let scoop = [];
	Array.prototype.smartJoin = function(sep=",") {
		let ans = "";
		if (this.length  === 1) {
			return this[0];
		}
		ans = this.slice(0, this.length - 1).join(sep);
		ans += ` and ${this[this.length - 1]}`;
		return ans
	}
</script>
	<main>
		<h2>Ice cream parlour:</h2>
		<h3>Ice creams: </h3>
		{#each store_icecreams as store_icecream}
			<div class="lefttext">
				<input type="checkbox" name="icecream" bind:group={icecream} value={store_icecream}/> {store_icecream}
			</div>
		{/each}
		<h3>Quantity: </h3>
		{#each store_scoops as store_scoop, i}
			<div class="lefttext">
				<input type=checkbox name="scoop" bind:group={scoop} value={store_scoop}/> {store_scoop} {store_scoop === 1? "scoop": "scoops"}
			</div>	
		{/each}
		{#if icecream.length > 0 && scoop.length > 0} 
			<h3>
				User wants
				{scoop} {scoop === 1 ? "scoop": "scoops"} of 
				{icecream.smartJoin(", ")}.
			</h3>
		{/if}
	</main>
		
<style>
	main {
		text-align: center;
		padding: 1em;
		max-width: 240px;
		margin: 0 auto;
	}

	.lefttext {
		width: 130px;
		margin: auto;
		text-align: left;
	}

	h1 {
		color: #ff3e00;
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