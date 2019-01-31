<template>
    <div class="filters">
        <p>валюта</p>
        <div class="buttons">
            <button v-for="(button, index) in buttons"
                    v-bind:key= "index"
                    >
               {{ button }}
            </button>
        </div>
        <p>количество пересадок</p>
        <ul class="transfers">
            <li v-for="transfer in transfers"
                       v-bind:key="transfer.name">
                <label 
                >
                    <input type="checkbox" 
                           name="transfer.name" 
                           :value="transfer.name"
                           v-model="transfer.checked" 
                           @click="onSelect(transfer.name)"
                           >
                    {{transfer.label}}
                </label>
            </li>
        </ul>
       <!--  {{selected}} -->
    </div>
    
</template>

<script >
    export default {
     //   props: ['selected'],
        data() {
            return {
                buttons : ['rub', 'usd', 'eur'],
                transfers : [
                     {
                        label : 'все',
                        name : 'all',
                        checked: false
                     }, 
                     {
                        label : 'без пересадок',
                        name : '0',
                         checked: false
                     }, 
                     {
                        label : '1 пересадка',
                        name : '1',
                        checked: false
                     },
                     {
                        label : '2 пересадки',
                        name : '2',
                         checked: false
                     },
                     {
                        label : '3 пересадки',
                        name : '3',
                        checked: false
                     }
                ]
    
            }
        },
        methods: {
            onSelect(num) {
                if (num === 'all') {
                    this.transfers.forEach(item => {
                        if (item.name != num) {
                            item.checked = false;
                        }
                    });
                } else {
                    this.transfers.forEach(item => {
                        if (item.name === "all") {
                            item.checked = false;
                        }
                    });
                }
                this.$emit('select', num);

            }
        }

    }
</script>

<style scoped lang="scss">
$btn-border-color: #d2d5d6;
$active-btn-color: #2196f3;
$btn-hover-color: #DADADA;
$text-color:#4A4A4A;

.filters {
    font-size: 12px;
    box-shadow: 0px 1px 4px 0px rgba(91,137,164,0.25);
    background-color: white;
    padding: 20px 15px;
    border-radius: 5px;
    height: max-content;
     p {
        text-transform: uppercase;
        color: $text-color;
        margin: 0;
        text-align: left;
    }

}
    .buttons {
        display: flex;
        margin: 15px 0;
        width: 100%;
        button {
            width: 33.3%;
            background-color: white;
            margin: 0;
            outline: none;
            border: 1px solid $btn-border-color;
            height:  40px;
            color: $active-btn-color;
            text-transform:uppercase;
            &:not(:last-child) {
                border-right-width: 0 ;
            }
            &:first-child {
                border-radius: 5px 0 0 5px;
            }
            &:last-child {
                border-radius: 0 5px 5px 0;
            }
            &:hover {
                cursor: pointer;
                background-color: $btn-hover-color;
            }
            &.avtive {
                background-color: $active-btn-color;
                border-color: $active-btn-color;
            }
        }
    }
   
    .transfers {
        display: flex;
        flex-direction: column;
        align-items: flex-start;

    }

</style>