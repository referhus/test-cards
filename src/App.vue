<template>
	<div id="app">
		<main class="container">
			<div class="search">
				<search-cmp
					@setSearch="setSearch"
				></search-cmp>
				<checkbox-cmp 
					:item="all" 
					class="all-checkbox"
					@setCheckbox="setAll"
				></checkbox-cmp>
			</div>
			<section class="cards">
				<template v-if="results.length">
					<card-cmp
						v-for="item in results" 
						:key="item.id" 
						:item="item"
					></card-cmp>
				</template>
				<template v-else>
					<card-cmp
						v-for="item in cards" 
						:key="item.id" 
						:item="item"
					></card-cmp>
				</template>
			</section>
		</main>
	</div>
</template>

<script>
	import cardCmp from './components/cardCmp.vue'
	import checkboxCmp from './components/checkboxCmp.vue'
	import searchCmp from './components/searchCmp.vue'

	export default {
		name: 'App',
		data: () => {
			return {
				cards: [
					{
						"id": 1,
						"price": "7 733 300 руб.",
						"type": {
							"icon": `<svg width="14" height="14" viewBox="0 0 14 14" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M8.99999 1.39999H12.6V12.6H1.39999V1.39999H4.59999L6.99999 2.99999M6.19999 12.6V6.99999M4.19999 6.99999H8.19999M10.6 6.99999H12.6" stroke="#808080"/></svg>`,
							"name": "Квартира",
							"desc": ""
						},
						"name": "Чистое Небо",
						"building": "10",
						"floor": 7,
						"apartment": 62,
						"area": 234.38,
						"rooms": 1,
						"address": "Лен. область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1",
						"image": "/assets/img.png",
						"date": "21/11/2020",
						"status": {
							"id": "entity",
							"name": "Уступка от юр.лица"
						},
						"checked": true
					},        
					{
						"id": 2,
						"price": "7 733 300 руб.",
						"type": {
							"icon": `<svg width="16" height="14" viewBox="0 0 16 14" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M2.86667 8.86669H5.66667M13.1333 8.86669H10.3333M3.8 6.06669H12.2M14.5333 6.06361V11.6667C14.5333 12.1822 14.1155 12.6 13.6 12.6H12.6667C12.1512 12.6 11.7333 12.1822 11.7333 11.6667V10.7334H4.26667V11.6667C4.26667 12.1822 3.8488 12.6 3.33333 12.6H2.4C1.88453 12.6 1.46667 12.1822 1.46667 11.6667V6.06361L3.4509 2.75874C3.95702 1.91576 4.86822 1.40002 5.85146 1.40002H10.1485C11.1318 1.40002 12.043 1.91576 12.5491 2.75874L14.5333 6.06361Z" stroke="#FF0D29"/></svg>`,
							"name": "Паркинг",
							"desc": "Подземная встроенно-пристроенная"
						},
						"name": "Зеленый квартал на Пулковских высотах",
						"building": "10",
						"quarter": "III",
						"year": "2022",
						"floor": 7,
						"apartment": 62,
						"area": 234.38,
						"rooms": 1,
						"address": "Комендантский пр., уч. 1 Каменка",
						"image": "/assets/img.png",
						"date": "21/11/2020",
						"status": {
							"id": "individual",
							"name": "Уступка от физ.лица"
						},
						"checked": false
					},
					{
						"id": 3,
						"price": "7 733 300 руб.",
						"type": {},
						"name": "Зеленый квартал на Пулковских высотах",
						"building": "10",
						"quarter": "III",
						"year": "2022",
						"area": 15,
						"number": "7-10-2 (ПИБ №68)",
						"address": "Лен. область, Всеволожский район, д. Кудрово, ул. Столичная, д. 5, к. 1",
						"image": "/assets/img.png",
						"date": "21/11/2020",
						"status": {
							"id": "booked",
							"name": "Забронировано"
						},
						"checked": false
					},
					{
						"id": 4,
						"price": "7 733 300 руб.",
						"type": {
							"icon": `<svg width="16" height="14" viewBox="0 0 16 14" fill="none" xmlns="http://www.w3.org/2000/svg"><path d="M2.86667 8.86669H5.66667M13.1333 8.86669H10.3333M3.8 6.06669H12.2M14.5333 6.06361V11.6667C14.5333 12.1822 14.1155 12.6 13.6 12.6H12.6667C12.1512 12.6 11.7333 12.1822 11.7333 11.6667V10.7334H4.26667V11.6667C4.26667 12.1822 3.8488 12.6 3.33333 12.6H2.4C1.88453 12.6 1.46667 12.1822 1.46667 11.6667V6.06361L3.4509 2.75874C3.95702 1.91576 4.86822 1.40002 5.85146 1.40002H10.1485C11.1318 1.40002 12.043 1.91576 12.5491 2.75874L14.5333 6.06361Z" stroke="#FF0D29"/></svg>`,
							"name": "Паркинг",
							"desc": "Подземная встроенно-пристроенная"
						},
						"name": "Зеленый квартал на Пулковских высотах",
						"building": "10",
						"quarter": "III",
						"year": "2022",
						"area": 15,
						"number": "7-10-2 (ПИБ №68)",
						"address": "Комендантский пр., уч. 1 Каменка",
						"image": "/assets/img.png",
						"date": "21/11/2020",
						"status": {
							"id": "done",
							"name": "Продано"
						},
						"checked": false
					}
				],
				all: {
					id: 0,
					label: 'все',
					checked: false
				},
				results: []
			}
		},
		components: {
			cardCmp,
			checkboxCmp,
			searchCmp
		},
		methods: {
			setElement(i) {
				this.cards.filter(item => item.id == i).length 
					&& (this.cards.filter(item => item.id == i)[0].checked = !this.cards.filter(item => item.id == i)[0].checked)
				this.cards.filter(item => item.checked).length === this.cards.length ? 
					this.all.checked = true : 
						this.all.checked = false
			},
			setAll() {
				this.all.checked = !this.all.checked
				this.all.checked ? 
					this.cards.map(item => item.checked = true) : 
						this.cards.map(item => item.checked = false)
			},
			setSearch(q) {
				this.results = this.cards.filter(item => item.name.toLowerCase().includes(q))
			}
		}
	}
</script>

<style>
	@import url('https://fonts.googleapis.com/css2?family=PT+Sans:wght@400;700&display=swap');
	:root {
		--gray: rgba(128, 128, 128, 1);
		--border: rgba(196, 196, 196, 1);
		--text: rgba(155, 155, 155, 1);
		--ind: rgba(2, 145, 193, 1);
		--entity: rgba(221, 76, 93, 1);
		--booked: rgba(104, 104, 104, 1);
		--fsxl: 15px;
		--fszm: 14px;
		--fszs: 13px;
		--fszxs: 12px;
		--lhm: 21px;
		--lhs: 20px;
	}

	* {
		margin: 0;
		padding: 0;
		box-sizing: border-box;
		font-family: 'PT Sans', sans-serif;
	}

	body {
		background: #F7F6F4;
	}

	.container {
		padding: 90px 20px 70px;
		max-width: 1040px;
		margin: 0 auto;
	}

	.cards {
		display: flex;
		flex-wrap: wrap;
		gap: 24px;
	}

	.search {
		margin-bottom: 40px;
	}

</style>
