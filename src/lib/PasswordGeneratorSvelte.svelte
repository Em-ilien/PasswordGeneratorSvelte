<script lang="ts">
	const options = {
		lower: true,
		upper: true,
		digit: true,
		symbol: true,
		lengthInput: 12
	};

	const generationPassword = () => {
		const lowers = options.lower ? 'abcdefghijklmnopqrstuvwxyz' : '';
		const uppers = options.upper ? 'ABCDEFGHIJKLMNOPQRSTUVWXYZ' : '';
		const digits = options.digit ? '0123456789' : '';
		const symbols = options.symbol ? '~#{[|\\^@]}&"\'(-_)=+?./!:;,' : '';
		const alf = lowers + uppers + digits + symbols;

		let code = '';
		for (let i = 0; i < options.lengthInput; i++)
			code += alf.charAt(Math.floor(Math.random() * alf.length));
		return code;
	};

	let password = generationPassword();

	let refreshActive = false;

	const refreshPassword = (event: Event) => {
		if (event.type === 'keydown' && (event as KeyboardEvent).key !== 'Enter') return;
		refreshActive = true;

		const animationTime = 0.325;
		setTimeout(() => (password = generationPassword()), (animationTime / 2) * 1000);
		setTimeout(() => (refreshActive = false), animationTime * 1000);
	};

	let copied = false;

	const copyPassword = (event: Event) => {
		if (event.type === 'keydown' && (event as KeyboardEvent).key !== 'Enter') return;
		navigator.clipboard.writeText(password);
		copied = true;
		setTimeout(() => (copied = false), 2000);
	};
</script>

<div class="password-generator">
	<div class={refreshActive ? 'refresh-active' : ''}>
		<input type="text" value={password} readonly />
		<div class="buttons">
			<div class="copy-container">
				<button class="copy" on:click={copyPassword} on:keydown={copyPassword}>
					<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 384 512">
						<!--!Font Awesome Free 6.6.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
						<path
							fill="currentColor"
							d="M280 64l40 0c35.3 0 64 28.7 64 64l0 320c0 35.3-28.7 64-64 64L64 512c-35.3 0-64-28.7-64-64L0 128C0 92.7 28.7 64 64 64l40 0 9.6 0C121 27.5 153.3 0 192 0s71 27.5 78.4 64l9.6 0zM64 112c-8.8 0-16 7.2-16 16l0 320c0 8.8 7.2 16 16 16l256 0c8.8 0 16-7.2 16-16l0-320c0-8.8-7.2-16-16-16l-16 0 0 24c0 13.3-10.7 24-24 24l-88 0-88 0c-13.3 0-24-10.7-24-24l0-24-16 0zm128-8a24 24 0 1 0 0-48 24 24 0 1 0 0 48z"
						/></svg
					>
				</button>
				{#if copied}
					<div class="copied-overlay">Copié !</div>
				{/if}
			</div>
			<button class="refresh" on:click={refreshPassword} on:keydown={refreshPassword}>
				<svg xmlns="http://www.w3.org/2000/svg" viewBox="0 0 512 512"
					><!--!Font Awesome Free 6.6.0 by @fontawesome - https://fontawesome.com License - https://fontawesome.com/license/free Copyright 2024 Fonticons, Inc.-->
					<path
						fill="currentColor"
						d="M105.1 202.6c7.7-21.8 20.2-42.3 37.8-59.8c62.5-62.5 163.8-62.5 226.3 0L386.3 160 352 160c-17.7 0-32 14.3-32 32s14.3 32 32 32l111.5 0c0 0 0 0 0 0l.4 0c17.7 0 32-14.3 32-32l0-112c0-17.7-14.3-32-32-32s-32 14.3-32 32l0 35.2L414.4 97.6c-87.5-87.5-229.3-87.5-316.8 0C73.2 122 55.6 150.7 44.8 181.4c-5.9 16.7 2.9 34.9 19.5 40.8s34.9-2.9 40.8-19.5zM39 289.3c-5 1.5-9.8 4.2-13.7 8.2c-4 4-6.7 8.8-8.1 14c-.3 1.2-.6 2.5-.8 3.8c-.3 1.7-.4 3.4-.4 5.1L16 432c0 17.7 14.3 32 32 32s32-14.3 32-32l0-35.1 17.6 17.5c0 0 0 0 0 0c87.5 87.4 229.3 87.4 316.7 0c24.4-24.4 42.1-53.1 52.9-83.8c5.9-16.7-2.9-34.9-19.5-40.8s-34.9 2.9-40.8 19.5c-7.7 21.8-20.2 42.3-37.8 59.8c-62.5 62.5-163.8 62.5-226.3 0l-.1-.1L125.6 352l34.4 0c17.7 0 32-14.3 32-32s-14.3-32-32-32L48.4 288c-1.6 0-3.2 .1-4.8 .3s-3.1 .5-4.6 1z"
					/></svg
				>
			</button>
		</div>
	</div>
	<div class="options">
		<div class="length">
			<label>
				<span>{options.lengthInput} caractères</span>
				<input
					type="range"
					min="4"
					max="30"
					bind:value={options.lengthInput}
					on:input={refreshPassword}
				/>
			</label>
		</div>
		<div class="characters">
			<label>
				<input type="checkbox" bind:checked={options.lower} on:change={refreshPassword} />
				Minuscules
			</label>
			<label>
				<input type="checkbox" bind:checked={options.upper} on:change={refreshPassword} />
				Majuscules
			</label>
			<label>
				<input type="checkbox" bind:checked={options.digit} on:change={refreshPassword} />
				Chiffres
			</label>
			<label>
				<input type="checkbox" bind:checked={options.symbol} on:change={refreshPassword} />
				Symboles
			</label>
		</div>
	</div>
</div>

<style>
	@import url('https://fonts.googleapis.com/css2?family=Inter:ital,opsz,wght@0,14..32,100..900;1,14..32,100..900&display=swap');

	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
	}

	.password-generator {
		font-family: 'Inter', sans-serif;
		background-color: white;
		border-radius: 15px;
		box-shadow: 0 6px 15px rgba(0, 0, 0, 0.1);
		padding: 25px;
		max-width: 600px;
		margin: 0 auto 40px;
		position: relative;
	}

	.password-generator > div {
		display: flex;
		align-items: center;
		justify-content: space-between;
	}

	.password-generator .buttons {
		display: flex;
		gap: 0.75em;
		margin-left: 0.75em;
	}

	.copy-container {
		position: relative;
		display: inline-block; /* Ensures that the overlay is positioned relative to this container */
	}

	.copied-overlay {
		position: absolute;
		top: 100%; /* Position it directly below the button */
		left: 50%;
		transform: translateX(-50%);
		background-color: #1e88e5aa;
		color: white;
		padding: 5px 10px;
		border-radius: 5px;
		font-size: 0.9rem;
		box-shadow: 0 4px 8px rgba(76, 175, 80, 0.3);
		animation: fade-in-out 2s ease-in-out;
		z-index: 10;
		white-space: nowrap;
		margin-top: 6px;
	}

	.copied-overlay::after {
		content: '';
		position: absolute;
		bottom: 100%;
		left: 50%;
		transform: translateX(-50%);
		border-width: 6px;
		border-style: solid;
		border-color: transparent transparent #1e88e5aa transparent;
	}

	@keyframes fade-in-out {
		0% {
			opacity: 0;
		}
		10%,
		90% {
			opacity: 1;
		}
		100% {
			opacity: 0;
		}
	}

	.password-generator input[type='text'] {
		width: 100%;
		padding: 12px;
		border: 2px solid #ddd;
		border-radius: 8px;
		font-size: 1.2rem;
		box-shadow: 0 2px 4px rgba(0, 0, 0, 0.1);
		font-family: monospace;
		letter-spacing: 0.2em;
	}

	.password-generator .refresh-active input[type='text'] {
		animation: fade-in 0.325s ease 1;
	}

	@keyframes fade-in {
		0% {
			color: #333;
		}
		45% {
			transform: translateY(-10px);
		}
		50% {
			color: #33333320;
		}
		55% {
			transform: translateY(5px);
		}
		100% {
			color: #333;
			transform: translateY(0);
		}
	}

	.password-generator .buttons button {
		width: 40px;
		height: 40px;
		padding: 0;
		background-color: #1e88e5;
		color: white;
		border: none;
		border-radius: 50%;
		box-shadow: 0 4px 8px rgba(30, 136, 229, 0.3);
		cursor: pointer;
		display: flex;
		align-items: center;
		justify-content: center;
		transition:
			background-color 0.3s ease,
			box-shadow 0.3s ease;
	}

	.password-generator .buttons button svg {
		width: 1.25em;
		height: 1.25em;
		color: white;
	}

	.password-generator .refresh-active .refresh svg {
		animation: rotate 0.325s linear 1;
	}

	@keyframes rotate {
		0% {
			transform: rotate(0deg);
		}
		100% {
			transform: rotate(360deg);
		}
	}

	.password-generator .refresh:hover,
	.password-generator .copy:hover {
		background-color: #1565c0;
		box-shadow: 0 6px 12px rgba(21, 101, 192, 0.4);
	}

	.password-generator .options {
		margin-top: 20px;
		gap: 2em;
	}

	.password-generator .options .length {
		flex-grow: 1;
	}

	.password-generator .options .length label span {
		width: 8em;
	}

	.password-generator .options .length label input {
		width: 15em;
	}

	.password-generator .options label {
		display: flex;
		align-items: center;
		gap: 0.375em;
		padding: 0.25em 0;
		font-weight: 500;
		width: max-content;
	}

	.password-generator .options label span {
		width: max-content;
	}

	.password-generator .options input[type='checkbox'],
	.password-generator .options input[type='range'] {
		margin-right: 10px;
	}

	.password-generator .options input[type='range'] {
		-webkit-appearance: none;
		width: 100%;
		height: 8px;
		background: #ddd;
		border-radius: 5px;
		outline: none;
		transition: background 0.3s ease;
	}

	.password-generator .options input[type='range']::-webkit-slider-thumb {
		-webkit-appearance: none;
		appearance: none;
		width: 20px;
		height: 20px;
		background: #1e88e5;
		border-radius: 50%;
		cursor: pointer;
		box-shadow: 0 4px 8px rgba(30, 136, 229, 0.3);
		transition:
			background 0.3s ease,
			box-shadow 0.3s ease;
	}

	.password-generator .options input[type='range']::-moz-range-thumb {
		width: 20px;
		height: 20px;
		background: #1e88e5;
		border-radius: 50%;
		cursor: pointer;
		box-shadow: 0 4px 8px rgba(30, 136, 229, 0.3);
		transition:
			background 0.3s ease,
			box-shadow 0.3s ease;
	}

	.password-generator .options input[type='checkbox'] {
		-webkit-appearance: none;
		appearance: none;
		width: 18px;
		height: 18px;
		background-color: #ddd;
		border: 2px solid #1e88e5;
		border-radius: 4px;
		cursor: pointer;
		position: relative;
		transition:
			background-color 0.3s ease,
			border-color 0.3s ease;
	}

	.password-generator .options input[type='checkbox']:checked {
		background-color: #1e88e5;
		border-color: #1e88e5;
	}

	.password-generator .options input[type='checkbox']::before {
		content: '\2713'; /* Symbole de coche (✓) */
		position: absolute;
		top: 50%;
		left: 50%;
		transform: translate(-50%, -50%) scale(0);
		font-size: 0.75rem;
		font-weight: bold;
		color: white;
		transition: transform 0.2s ease;
	}

	.password-generator .options input[type='checkbox']:checked::before {
		transform: translate(-50%, -50%) scale(1);
	}

	.password-generator .options input[type='range']:hover::-webkit-slider-thumb,
	.password-generator .options input[type='range']:hover::-moz-range-thumb {
		background: #1565c0;
		box-shadow: 0 6px 12px rgba(21, 101, 192, 0.4);
	}
</style>
