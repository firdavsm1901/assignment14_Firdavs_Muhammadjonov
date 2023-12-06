	<template>

		<header>
			<h1>TIC-TAC-TOE</h1>
		</header>
		<TurnIndicator v-show="!isEnded" :turnNum="turn" />
		<WinIndicator v-show="isEnded" :turnNum="turn" :isTie="isTie" />
		<div class="cont-slot">
			<MarkSlot
			v-for="slotID in 9"
			:key="slotID - 1"
			@slot-clicked="onMarkSlotClick(slotID - 1)"
			:turnNum="board[slotID - 1]"
			:id="slotID - 1"
			:winningCombination="winningCombination"
			/>
		</div>
		<button id="btn-reset" @click="resetBoard">Reset</button>

	</template>
	
	<script>
	import MarkSlot from "./components/MarkSlot.vue";
	import TurnIndicator from "./components/TurnIndicator.vue";
	import WinIndicator from "./components/WinIndicator.vue";
	
	export default {
		name: "App",
		components: {
		MarkSlot,
		TurnIndicator,
		WinIndicator,
		},
		data() {
		return {
			turn: 0,
			board: [-1, -1, -1, -1, -1, -1, -1, -1, -1],
			isEnded: false,
			isTie: false,
			winningCombination: [], 
		};
		},
		methods: {
		resetBoard() {
			this.board = [-1, -1, -1, -1, -1, -1, -1, -1, -1];
			this.turn = 0;
			this.isEnded = false;
			this.isTie = false;
			this.winningCombination = [];
		},
		onMarkSlotClick(id) {
			if (this.isEnded || this.board[id] !== -1) {
			return;
			}
	
			let mark = this.turn % 2;
			this.board[id] = mark;
	
			const winningCombinations = [
			[0, 1, 2], [3, 4, 5], [6, 7, 8], 
			[0, 3, 6], [1, 4, 7], [2, 5, 8], 
			[0, 4, 8], [2, 4, 6],
			];
	
			for (const combo of winningCombinations) {
			const [a, b, c] = combo;
			if (this.board[a] === mark && this.board[b] === mark && this.board[c] === mark) {
				this.isEnded = true;
				this.winningCombination = combo; 
				break;
			}
			}
	
			if (!this.isEnded && this.turn >= 8) {
			this.isEnded = true;
			this.isTie = true;
			}
	
			if (!this.isEnded) {
			this.turn += 1;
			}
		},
		},
	};
	</script>
	

	


	<style>
	@font-face {
		font-family: "Iosevka Aile Lite";
		src: "./assets/font/iosevka-aile-lite-regular.ttf"
	}

	* {
		--clr-fg: #fecea8;
		--clr-bg: #2a363b;
		--clr-acc: #99b898;
		--clr-acc-x: #4e92b5;
		--clr-acc-o: #b54e4e;
		--clr-faded: #5d6468;
		font-family: "Iosevka Aile Lite", sans-serif;
		-webkit-font-smoothing: antialiased;
		-moz-osx-font-smoothing: grayscale;
	}
	body {
	background: #364e58;
	}

	h1 {
		color: var(--clr-bg);
		background-color: var(--clr-acc);
		padding: 0 1em;
		margin-top: 0;
		margin-bottom: 0.5em;
	}

	button {
		font-size: 1rem;
		color: var(--clr-bg);
		background-color: var(--clr-acc);
		cursor: pointer;
		width: fit-content;
		padding: 0.5em;
		border: 0;
		border-radius: 0.2em;
		margin: 0.2em;
	}

	#app {
		color: var(--clr-fg);
		display: flex;
		flex-direction: column;
		align-items: center;
		width: fit-content;
		border-radius: 0.2em;
		margin: 0 auto;
		margin-top: 60px;
		box-shadow: 0 0 30px rgba(0, 0, 0, 0.2);
		background-color: var(--clr-bg);
	}

	.cont-ind {
		font-size: 1.5rem;
		display: flex;
		align-items: center;
		margin-bottom: 0.5em;
	}

	.cont-slot {
		display: grid;
		grid-template-columns: repeat(3, 1fr);
		grid-template-rows: repeat(3, 1fr);
		width: fit-content;
		margin-bottom: 0.5em;
	}

	#btn-reset {
		font-weight: 700;
		padding: 0.5em 3em;
		margin-bottom: 1em;
	}

	.highlight {
		background-color: #ffd700;
	}

	</style>