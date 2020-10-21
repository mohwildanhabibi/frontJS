<template>
	<v-data-table
		:headers="headers"
		:items="context"
		:items-per-page="per_page"
		:page="page"
		class="elevation-1"
		:footer-props="{
			'items-per-page-options': [6, 12, 18, -1],
		}"
	>
		<template v-slot:item.avatar="{ item }">
            <div>
              	<v-img :src="item.avatar" :alt="item.avatar" height="100px" width="100px"></v-img>
            </div>
        </template>
	</v-data-table>
</template>

<script>
export default {
	async asyncData({ $axios }) {
		const fetch = await $axios.$get('http://localhost:3001/users')
		// console.log(fetch);
		return {
        headers: [
			{ text: 'ID', value: 'id' },
			{ text: 'Email', value: 'email' },
			{ text: 'First Name', value: 'first_name' },
			{ text: 'Last Name', value: 'last_name' },
			{ text: 'Avatar', value: 'avatar' },
		],
		context: fetch.data,
		per_page: fetch.per_page,
		page: fetch.page,
     	}
    },      
};
</script>
