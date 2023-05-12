<template>
    <div class="search-container">
        <svg width="38" height="24" viewBox="0 0 38 24" fill="none" xmlns="http://www.w3.org/2000/svg">
            <path d="M26 19L22 15M18 17C14.6863 17 12 14.3137 12 11C12 7.68629 14.6863 5 18 5C21.3137 5 24 7.68629 24 11C24 14.3137 21.3137 17 18 17Z" stroke="#9B9B9B" stroke-width="1.5"/>
        </svg>
        <input 
            v-model="query" 
            type="text" 
            placeholder="Введите ЖК / корпус / № квартиры / № паркинга"
            @input="$emit('setSearch', query)"
        >

    </div>
</template>

<script>
    export default {
        data() {
            return {
                query: ''
            }
        },
    }
</script>

<style>
    .search-container {
        display: flex;
        border: 1px solid var(--border);
        padding: 7px 11px;
        gap: 23px;
        font-size: var(--fszm);
        color: var(--text);
        margin-bottom: 30px;
    }

    .search-container input {
        border: none;
        background: transparent;
        width: calc(100% - 37px - 23px);
        outline: none;
    }

</style>