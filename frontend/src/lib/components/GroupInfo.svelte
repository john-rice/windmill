<script lang="ts">
	import { GroupService } from '$lib/gen'
	import { workspaceStore } from '$lib/stores'
	import Popover from './Popover.svelte'

	export let name: string

	$: $workspaceStore && loadMembers()

	let members: string[] | undefined = []

	async function loadMembers() {
		members = (await GroupService.getGroup({ workspace: $workspaceStore!, name })).members
	}
</script>

{#if members}
	<Popover
		><div class="inline-flex gap-1 items-end"
			><span class="text-tertiary text-xs">({members.length})</span>
			<div class="max-w-xs truncate"
				><span class="text-tertiary text-xs">{members?.join(', ')}</span></div
			></div
		>
		<span slot="text">{members?.join(', ')}</span></Popover
	>
{/if}
