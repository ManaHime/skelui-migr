<script lang="ts">
	import '../app.css';
	import { Navigation } from '@skeletonlabs/skeleton-svelte';
	import { page } from '$app/stores';
	import { onMount } from 'svelte';
	import { check } from '@tauri-apps/plugin-updater';

	// Floating UI for Popups
	import { computePosition, autoUpdate, flip, shift, offset, arrow } from '@floating-ui/dom';

	interface Props {
		children?: import('svelte').Snippet;
	}

	let { children }: Props = $props();

	onMount(() => {
		const savedTheme = localStorage.getItem('theme') || 'dark'; // Set default to dark
		document.documentElement.classList.remove('dark', 'light');
		document.documentElement.classList.add(savedTheme);
	});

	onMount(() => {
		document.addEventListener('contextmenu', (event) => {
			event.preventDefault();
		});
	});

	const setTheme = (theme: string) => {
		document.documentElement.classList.remove('dark', 'light');
		document.documentElement.classList.add(theme);
		localStorage.setItem('theme', theme);
	};

	let updateStatus = $state<'unknown' | 'unavailable' | 'available'>('unknown');
	async function checkForUpdate() {
		try {
			const update = await check();
			if (update?.available) {
				updateStatus = 'available';
			} else {
				updateStatus = 'unavailable';
			}
		} catch (error) {
			console.error('アップデートの確認に失敗しました。', error);
		}
	}
	async function ignoreUpdate() {
		updateStatus = 'unavailable';
	}
	checkForUpdate();
	let value = $state('0');
</script>

<!-- App Shell -->
<Navigation.Bar {value} onValueChange={(_value) => (value = _value)}>
	<Navigation.Tile id="0" label="売り上げ" href="/" selected={$page.url.pathname === '/'}
	></Navigation.Tile>
		<Navigation.Tile
		id="1"
		label="設定"
		href="/settings"
		selected={$page.url.pathname === '/settings'}
	></Navigation.Tile>
</Navigation.Bar>


	{@render children?.()}

