<script>
	let store_icecreams = ["Vanilla", "Chocochip", "Mint Cookie", "Mango", "Caramel Salted"];
	let cart = {};
	let icecreamselection = function (event) {
		if (event.target.checked) {
			cart[event.target.value] = 1;
		} else {
			cart[event.target.value] = undefined;
		}
	}

	let updateqty = function(event) {
		let item = event.target.getAttribute("data-key");
		cart[item] = event.target.value;
	}
	Array.prototype.smartJoin = function(sep=",") {
		let ans = "";
		if (this.length  === 1) {
			return this[0];
		}
		ans = this.slice(0, this.length - 1).join(sep);
		ans += ` and ${this[this.length - 1]}`;
		return ans
	}

	Object.prototype.smartJoin = function () {
		let newarr = [];
		Object.keys(this).forEach(item => {
			let qty = this[item];
			if (+qty > 0) {
				newarr.push(`${this[item]} ${this[item] === 1 ? "scoop": "scoops"} of ${item}` );
			} 
		});
		return newarr;
	}


</script>
	<main>
		<h2>Ice cream parlour:</h2>
		<h3>Ice creams: </h3>
		{#each store_icecreams as store_icecream}
			<div class="icecream-div">
				<div class="icecreamoption">
					<input class="checkboxelement" type="checkbox" name="icecream"  on:change={icecreamselection} value={store_icecream}/> {store_icecream}
				</div>
				{#if cart[store_icecream] !== undefined} 
					<div class="qtyoption">
						<input class="inputelement" data-key={store_icecream} on:input={updateqty} type="number" value={cart[store_icecream]} />
					</div>
				{/if}
			</div>
		{/each}
		
		{#if cart.smartJoin().length > 0} 
			<h3>
				User wants
				{cart.smartJoin().smartJoin(", ")}.
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

	.checkboxelement {
		position: relative;
	}
	.icecream-div {
		padding: 0px;
		width: 300px;
		height: 40px;
		margin: auto;
		text-align: left;
	}
	.icecreamoption {
		text-align: left;
		height: 100%;
		width: 60%;
		float: left;
	
	}

	.qtyoption {
		width: 35%;
		height: 100%;
		float: left;
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