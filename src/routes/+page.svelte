<script lang="ts">
	import * as accordion from '@zag-js/accordion';
	import { normalizeProps, useMachine } from '$lib/dist/index.js';
	import { unstate } from 'svelte';

	const data = [
		{ title: 'Watercraft', content: 'Sample accordion content' },
		{ title: 'Automobiles', content: 'Sample accordion content' },
		{ title: 'Aircrafts', content: 'Sample accordion content' }
	];

	const machine = useMachine(accordion.machine({ id: '1' }));

	const api = $derived(accordion.connect(unstate(machine.state), machine.send, normalizeProps));
</script>

<div {...api.rootProps}>
	{#each data as item}
		<div {...api.getItemProps({ value: item.title })}>
			<h3>
				<button {...api.getItemTriggerProps({ value: item.title })}>
					{item.title}
				</button>
			</h3>
			<div {...api.getItemContentProps({ value: item.title })}>
				{item.content}
			</div>
		</div>
	{/each}
</div>
