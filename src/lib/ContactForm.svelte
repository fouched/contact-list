<script>
	import { onDestroy } from 'svelte'
	import contactStore from '../stores/contact'

	let name = ''
	let phone = ''

	$: title = $contactStore.editId ? 'Edit Contact' : 'Add Contact'

	const onSubmit = () => {

		if ($contactStore.editId === undefined) {
			contactStore.add(name, phone)
		} else {
			contactStore.edit($contactStore.editId, name, phone)
		}	

		name = ''
		phone = ''
	}

	const unsub = contactStore.subscribe(({ contacts, editId }) => {
		if (!editId) return

		const contact = contacts.find(c => c.id === editId)
		name = contact.name
		phone = contact.phone
	})

	onDestroy(() => {
		unsub()
	})

</script>
<h1 class="text-2xl">Contact Form</h1>
<h2 class="text-lg mt-4 mb-2">{title}</h2>
<form on:submit|preventDefault={onSubmit} >
	<div class="mb-1">
		<label for="fullName" class="text-sm">Name</label>
	</div>	
	<div class="mb-1">
		<input type="text" name="fullName" id="fullName" 
			bind:value={name} 
			class="text-sm px-1 border-gray-300 border-2 rounded-md 
				focus:outline-none focus:border-blue-400" 
			placeholder="Full Name">
	</div>
	<div class="mb-1">
		<label for="fullName" class="text-sm">Number</label>
	</div>
	<div class="mb-3">
		<input type="text" name="number" id="number" 
			bind:value={phone}
			class="text-sm px-1 border-gray-300 border-2 rounded-md 
				focus:outline-none focus:border-blue-400" 
			placeholder="Phone">
	</div>

	<div><button class="text-sm bg-green-500 text-white rounded-md px-3 py-1">{title}</button></div>


</form>