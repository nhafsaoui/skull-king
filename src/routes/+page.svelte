<script>
	import myshades from '$lib/utils/myshades';
	import { onMount } from 'svelte';

	let audio = null;

	const playSound = () => {
		if (!audio) {
			audio = new Audio('/sounds/skull-king.mp3');
			audio.play();
		} else {
			audio.play();
		}
	};

	const changePalette = () => {
		let primary = `#${Math.floor(Math.random() * 16777215).toString(16)}`;

		if (primary.length < 7) {
			primary = primary.padEnd(7, '0');
		}

		console.log('Initial Color selected', primary);

		myshades({
			primary
		});
	};
</script>

<main class="home">
	<img
		on:click={() => {
			playSound();
			changePalette();
		}}
		src="/skullking.svg"
		alt="SkullKing"
	/>

	<div class="main-menu">
		<a href="/create">Create A New Game</a>
		<a href="/history">History</a>
	</div>

	<div class="logout-container">
		<button class="logout-btn" on:click={() => {
			window.localStorage?.removeItem?.('team-name')
			location.reload();
		}}>
			<svg width="20" height="20" viewBox="0 0 20 20" fill="none" xmlns="http://www.w3.org/2000/svg" style="vertical-align:middle;margin-right:8px;"><path d="M7.5 3.333V5a.833.833 0 0 0 1.667 0V3.333A3.333 3.333 0 0 1 12.5 6.667v6.666a3.333 3.333 0 0 1-3.333 3.334V15a.833.833 0 0 0-1.667 0v1.667A5 5 0 0 0 15 13.333V6.667A5 5 0 0 0 7.5 3.333Z" fill="#fff"/><path d="M2.5 10a.833.833 0 0 1 .833-.833h7.5a.833.833 0 1 1 0 1.666h-7.5A.833.833 0 0 1 2.5 10Z" fill="#fff"/></svg>
			Log out
		</button>
	</div>
</main>

<style lang="scss">
	.logout-container {
		display: flex;
		justify-content: center;
	}

	.logout-btn {
		display: flex;
		align-items: center;
		gap: 8px;
		background: linear-gradient(90deg, #e52d27 0%, #b31217 100%);
		color: #fff;
		border: none;
		border-radius: 25px;
		padding: 12px 28px;
		font-size: 1.1rem;
		font-weight: 600;
		box-shadow: 0 2px 8px rgba(0,0,0,0.08);
		cursor: pointer;
	}

	.home {
		display: flex;
		flex-direction: column;
		align-items: center;
		justify-content: center;
		height: 100vh;
		cursor: pointer;

		h1 {
			color: var(--primary-950);
		}
	}
	.main-menu {
		height: 50dvh;
		display: flex;
		justify-content: center;
		flex-direction: column;
		margin-top: 20px;
		align-items: center;
		gap: 10px;
		font-size: 1.5rem;
	}

	.main-menu a {
		margin: 0 10px;
		text-decoration: none;
		background-color: white;
		color: var(--primary-950);
		padding: 10px 20px;
		border-radius: 5px;
		width: 80vw;
		text-align: center;
	}
</style>
