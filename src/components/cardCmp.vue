<template>
    <div class="card">
        <div class="card-checkbox">
            <checkbox-cmp 
                :item="item"
                @setCheckbox="setCheckbox"
            ></checkbox-cmp>
        </div>
        <div class="card-content">
            <div class="card-left">
                <div class="card-content-head">
                    <div class="card-price"> {{ item.price }} </div>
                    <div 
                        v-if="item.type.name" 
                        class="card-type" 
                        @mousemove="open = true" 
                        @mouseleave="open = false"
                    > 
                        <div class="card-type-icon" v-html="item.type.icon"></div>
                        <div class="card-type-name">
                            {{ item.type.name }} 
                        </div>
                        <div class="card-type-desc" v-if="item.type.desc && open">
                            {{ item.type.desc }}
                        </div>
                    </div>
                    <div 
                        class="card-status"
                        :class="item.status.id"
                    > 
                        <span> {{ item.status.name }} </span> 
                    </div>
                    <div class="card-name">
                        <span> {{ item.name }},</span>
                        <span v-if="item.building"> {{ item.building }} корпус, </span>
                        <span v-if="item.quarter"> {{ item.quarter }} кв. </span>
                        <span v-if="item.year"> {{ item.year }} г. </span>
                    </div>
                </div>
                <div class="card-params">
                    <div class="card-param">
                        <div v-if="item.apartment"> кв. {{ item.apartment }}  </div>
                        <div v-if="item.rooms"> {{ item.rooms }} комн. кв. </div>
                        <div v-if="item.number"> № {{ item.number }} </div>
                    </div>
                    <div class="card-param">
                        <div v-if="item.area"> {{ item.area }} м2 </div>
                        <div v-if="item.floor"> {{ item.floor }} этаж </div>
                    </div>
                </div>
                <div class="card-address"> 
                    <svg width="13" height="13" viewBox="0 0 13 13" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M6.5 0C3.97993 0 1.92969 2.05024 1.92969 4.57031C1.92969 5.42176 2.16554 6.2527 2.61191 6.97359L6.23985 12.82C6.30934 12.932 6.43178 13 6.56345 13C6.56447 13 6.56546 13 6.56647 13C6.69929 12.999 6.82198 12.9288 6.8902 12.8149L10.4257 6.91184C10.8474 6.20618 11.0703 5.3965 11.0703 4.57031C11.0703 2.05024 9.02007 0 6.5 0ZM9.77199 6.52077L6.55769 11.8875L3.25932 6.57226C2.88778 5.97223 2.68633 5.27998 2.68633 4.57031C2.68633 2.47025 4.39994 0.756641 6.5 0.756641C8.60006 0.756641 10.3111 2.47025 10.3111 4.57031C10.3111 5.25893 10.123 5.93348 9.77199 6.52077Z" fill="#9B9B9B"/>
                        <path d="M6.5 2.28516C5.23996 2.28516 4.21484 3.31028 4.21484 4.57031C4.21484 5.8223 5.22328 6.85547 6.5 6.85547C7.79246 6.85547 8.78516 5.80854 8.78516 4.57031C8.78516 3.31028 7.76004 2.28516 6.5 2.28516ZM6.5 6.09883C5.65558 6.09883 4.97148 5.41244 4.97148 4.57031C4.97148 3.73029 5.65998 3.0418 6.5 3.0418C7.34002 3.0418 8.02598 3.73029 8.02598 4.57031C8.02598 5.40015 7.3578 6.09883 6.5 6.09883Z" fill="#9B9B9B"/>
                    </svg>
                    <span> {{ item.address }} </span>
                </div>
            </div>
            <div class="card-right">
                <img class="card-image" :src="item.image" alt="card-image" />
                <div class="card-date">Добавлено {{ item.date }}</div>
            </div>
        </div>
    </div>
</template>

<script>
    import checkboxCmp from './checkboxCmp.vue'

    export default {
        name: 'App',
        props: ['item'],
        data: () => {
            return {
                open: false,
            }
        },
        components: {
            checkboxCmp
        },
        methods: {
            setCheckbox(i) {
                this.$parent.setElement(i)
            }
        }
    }
</script>

<style>
    .card {
    width: calc(50% - var(--fszxs));
    height: 238px;
    gap: 6px;
    padding: 25px;
    display: flex;
    position: relative;
    align-items: center;
    border: 1px solid #E5E5E5;
    background: white;
    justify-content: space-between;
    }

    .card-right {
        align-self: flex-end;
    }

    .card-left {
        display: flex;
        flex-direction: column;
    }

    .card-checkbox {
    width: 16px;
    }

    .card-content {
        width: calc(100% - 16px - 25px);
        display: flex;
        justify-content: space-between;
        height: 100%;
    }

    .card-content-head {
        gap: 6px 16px;
        display: grid;
        max-width: 227px;
        grid-template-areas: 
        'price type'
        'name name';
    }

    .card-price {
        color: #FF0D29;
        font-size: var(--fszl);
        font-weight: 700;
        grid-area: price;
    }

    .card-type {
        display: flex;
        align-items: center;
        gap: 8px;
        box-shadow: 0px 0px 2px rgba(94, 119, 157, 0.25);
        border-radius: 32px;
        padding: 5px 16px;
        font-size: var(--fszxs);
        line-height: 16px;
        position: relative;
        cursor: pointer;
        grid-area: type;
    }

    .card-type-icon {
        width: 14px;
        height: 14px;
    }

    .card-type-desc {
        position: absolute;
        bottom: -50px;
        background: #2D2D2D;
        opacity: 0.7;
        color: white;
        padding: 12px 18px;
        font-size: var(--fszs);
        line-height: var(--lhs);
        white-space: nowrap;
    }

    .card-status {
        padding: 6px 9px;
        max-width: 151px;
        position: absolute;
        right: 0;
        top: 21px;
    }

    .card-status span {
        position: relative;
        padding-left: 14px;
        font-size: var(--fszm);
        white-space: nowrap;
    }

    .card-status span::before {
        content: '';
        position: absolute;
        width: 6px;
        height: 6px;
        top: 40%;
        left: 0;
        border-radius: 50%;
    }

    .card-name {
        font-size: var(--fszm);
        line-height: var(--lhm);
        color: var(--gray);
        max-width: 218px;
        width: 100%;
        grid-area: name;
    }

    .card-name span:first-child {
        color: black;
    }

    .card-params {
        display: flex;
        max-width: 218px;
        width: 100%;
        font-size: var(--fszm);
        line-height: var(--lhm);
        margin: auto;
    }

    .card-param:nth-child(even) {
        padding-left: 20px;
        margin-left: 20px;
        border-left: 1px solid var(--border);
    }

    .card-address {
        max-width: 218px;
        position: relative;
        font-size: var(--fszm);
        line-height: var(--lhm);
    }

    .card-address svg {
        position: absolute;
        left: -20px;
        top: 5px
    }

    .card-date {
        font-size: var(--fszs);
        line-height: var(--lhs);
        color: var(--text)
    }

    .individual {
        color: var(--ind);
        background: rgba(214, 245, 255, 1);
    }

    .individual span::before {
        background: var(--ind);
    }

    .entity {
        color: var(--entity);
        background: rgba(255, 228, 228, 1);
    }

    .entity span::before {
        background: var(--entity);
    }

    .done {
        color: var(--gray);
        background: rgba(204, 204, 204, 1);
    }

    .done span::before {
        background: var(--gray);
    }

    .booked {
        color: var(--booked);
        background: rgba(237, 237, 237, 1);
    }

    .booked span::before {
        background: var(--booked);
    }

    @media screen and (max-width: 1024px) {
        .card {
            width: 100%;
        }
    }

</style>
