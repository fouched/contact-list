<script>
	import contactStore from '../stores/contact'

	const onDelete = (contactId) => {
		contactStore.delete(contactId)
	}

	const onEdit = (contactId) => {
		contactStore.editContact(contactId)
	}

</script>
<h1 class="text-xl mt-6">Contact List</h1>
<div class="grid grid-cols-3 py-2 text-sm">
	{#each $contactStore.contacts as contact (contact.id)}
	<div class="col-span-3 py-1"><hr /></div>
		<div class="px-2 py-1">
			{contact.name}
		</div>
		<div class="px-2 py-1">
			{contact.phone}
		</div>
		<div class="flex justify-end space-x-2">
			<button class="px-3 py-1 bg-green-500 text-white rounded-md"
				on:click={() => onEdit(contact.id)}>Edit</button>
			<button class="px-3 py-1 bg-red-500 text-white rounded-md"
				on:click={() => onDelete(contact.id)}
			>Delete</button>
		</div>			
	{/each}

</div>
<hr>
