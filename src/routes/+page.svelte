<script lang="ts">
	let userInput = $state('');


	const resetValues = () => {
		userInput = '';
	};
</script>

{#snippet loadingBlock()}
	<div class="flex flex-col items-center my-2">
		<section class="flex items-center w-full max-w-xl p-2 space-y-2 rounded-sm card">
			<div class="flex items-center max-w-xl">
				<div class="p-4 space-y-4">
					<div class="grid grid-cols-4">
						<div class="placeholder animate-pulse w-28"></div>
						<div class="w-32 placeholder animate-pulse"></div>
						<div class="placeholder animate-pulse w-30"></div>
						<div class="placeholder animate-pulse w-30"></div>
					</div>
					<div class="grid grid-cols-1 gap-6">
						<div class="w-64 placeholder animate-pulse"></div>
						<div class="placeholder animate-pulse w-72"></div>
						<div class="placeholder animate-pulse w-80"></div>
					</div>
					<div class="grid grid-cols-1 gap-4">
						<div class="placeholder animate-pulse w-80"></div>
						<div class="placeholder animate-pulse w-72"></div>
					</div>
					<div class="grid grid-cols-1 gap-4">
						<div class="placeholder animate-pulse w-76"></div>
						<div class="placeholder animate-pulse w-72"></div>
						<div class="placeholder animate-pulse w-80"></div>
						<div class="placeholder animate-pulse w-76"></div>
						<div class="placeholder animate-pulse w-72"></div>
						<div class="placeholder animate-pulse w-80"></div>
					</div>
					<div class="grid grid-cols-1 gap-4">
						<div class="placeholder animate-pulse w-80"></div>
						<div class="placeholder animate-pulse w-76"></div>
						<div class="placeholder animate-pulse w-72"></div>
					</div>
					<div class="grid grid-cols-1 gap-4">
						<div class="placeholder animate-pulse w-76"></div>
						<div class="placeholder animate-pulse w-72"></div>
						<div class="placeholder animate-pulse w-80"></div>
						<div class="placeholder animate-pulse w-76"></div>
						<div class="placeholder animate-pulse w-72"></div>
						<div class="placeholder animate-pulse w-80"></div>
					</div>
				</div>
			</div>
		</section>
	</div>
{/snippet}

<div class="flex flex-col items-center my-2">
	<div class="flex w-full max-w-xl">
		<!-- Input -->
		<textarea
			placeholder="ここに入力してください
どこでものの番号でいいよの番号もいい：例0232-1234-3443"
			bind:value={userInput}
			class="w-full h-16 overflow-hidden resize-none input textarea"
		></textarea>
		<button
			type="button"
			class="rounded-sm btn variant-filled-secondary"
			onclick={() => resetValues()}
		>
			新規
		</button>
	</div>
</div>
