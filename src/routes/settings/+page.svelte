<script lang="ts">
	import { getVersion } from '@tauri-apps/api/app';
	import { check } from '@tauri-apps/plugin-updater';
	import { relaunch } from '@tauri-apps/plugin-process';

	let updateMessage = $state('アップデートを確認しています...');
	let updateStatus = $state<'unknown' | 'unavailable' | 'available'>('unknown');

	let appVersion = $state('');
	let isUpdateUnavailable = $derived(updateStatus === 'unavailable');

	async function checkForUpdate() {
		try {
			const update = await check();
			if (update?.available) {
				updateMessage = `新しいバージョン ${update.version} が利用可能です。`;
				updateStatus = 'available';
			} else {
				updateMessage = '最新のバージョンを使用しています。';
				updateStatus = 'unavailable';
			}
		} catch (error) {
			updateMessage = 'アップデートの確認に失敗しました。' + error;
		}
	}

	const getAppVersion = async () => {
		try {
			return (appVersion = await getVersion());
		} catch (error) {
			updateMessage = 'アプリのバージョンを取得できませんでした。' + error;
		}
	};

	getAppVersion();

	const doUpdate = async () => {
		try {
			const update = await check();
			updateMessage = 'アップデートをダウンロードしています...';
			await update?.downloadAndInstall();
			updateMessage = 'アップデートが完了しました。アプリを再起動しています...';
			await relaunch();
		} catch (error) {
			updateMessage = 'アップデートをできませんでした。' + error;
		}
	};

	const setTheme = (theme: string) => {
		document.documentElement.classList.remove('dark', 'light');
		document.documentElement.classList.add(theme);
		localStorage.setItem('theme', theme);
	};

	// Handle theme switch event
	function toggleTheme() {
		const currentTheme = document.documentElement.classList.contains('dark') ? 'light' : 'dark';
		document.documentElement.classList.remove('dark', 'light');
		document.documentElement.classList.add(currentTheme);
		localStorage.setItem('theme', currentTheme);
	}
</script>

<div class="flex flex-col items-center gap-4 my-2">
	<div class="flex flex-col items-center w-full max-w-xl gap-4 p-4 card">
		<p class="text">現在のバージョン: {appVersion}</p>
		<p class="text">{updateMessage}</p>
		{#if updateStatus === 'available'}
			<button class="p-2 rounded-sm btn variant-filled-primary" onclick={doUpdate}
				>インストール</button
			>
		{:else}
			<button
				class="p-2 rounded-sm btn variant-filled-secondary"
				onclick={checkForUpdate}
				disabled={isUpdateUnavailable}
			>
				アップデートを確認
			</button>
		{/if}
	</div>
	<div class="flex flex-col items-center w-full max-w-xl gap-4 p-4 card">
		<button onclick={toggleTheme} class="p-2 bg-gray-200 border rounded-sm btn dark:bg-gray-800">
			ダーク / ライト モード
		</button>
	</div>
</div>
