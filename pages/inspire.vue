<template>
	<v-data-table
		:headers="headers"
		:items="dataTabel"
		:items-per-page="per_page"
		:page="page"
		class="elevation-1"
		hide-default-footer
	>
		<template v-slot:item.avatar="{ item }">
			<div>
				<v-img :src="item.avatar" :alt="item.avatar" height="100px" width="100px"></v-img>
			</div>
		</template>
		<template v-slot:footer>
			<hr>
			<div class="text-center pt-2">
				<v-pagination v-model="thisPage" :length="page"></v-pagination>
			</div>
		</template>
	</v-data-table>
</template>

<script>
import axios from 'axios'
export default {
	async created () {
		await this.getData(1)
	},
	data () {
		return {
			thisPage: 1,
			page: 2,
			dataTabel: [],
			per_page: 6,
			headers: [
				{ text: 'ID', value: 'id' },
				{ text: 'Email', value: 'email' },
				{ text: 'First Name', value: 'first_name' },
				{ text: 'Last Name', value: 'last_name' },
				{ text: 'Avatar', value: 'avatar' },
			],
		}
	},
	methods: {
		async getData(page) {
			const getData = await axios.get('http://localhost:3001/users/'+page)
			if (getData.status === 200) {
				this.dataTabel = getData.data.data
			}
		},
		resetData () {
			this.dataTabel = []
		}
	},
	watch :{
		async thisPage() {
			this.resetData()
			await this.getData(this.thisPage)
		}
	}
};
</script>
