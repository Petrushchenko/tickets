<template>
    <div class='filters'>
        <p>валюта</p>
        <div class="buttons">
            <button v-for="(button, index) in buttons"
                    v-bind:key= "index"
                    :class="{active : currency == button}"
                    @click = "changeCurrency(button)"
                    >
               {{ button }}
            </button>
        </div>
        <p>количество пересадок</p>
        <ul class="transfers">
            <li v-for="transfer in transfers"
                v-bind:key="transfer.name">
                <label :class="{ checked: transfer.checked}"
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
    </div>
    
</template>

<script >
    export default {
       
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
                ],
                currency: 'rub'
    
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
            },
            changeCurrency(str) {
                this.currency = str;
                this.$emit('onChangeCurrency', this.currency);
            }
        },
    }
</script>

<style scoped lang="scss">
$btn-border-color: #d2d5d6;
$active-btn-color: #2196f3;
$btn-hover-color:  #f2fcff;
$text-color:#4A4A4A;
* {
    box-sizing: border-box;
}

.filters {
    font-size: 12px;
    box-shadow: 0px 1px 4px 0px rgba(91,137,164,0.25);
    background-color: white;
    padding: 20px 0;
    border-radius: 5px;
    height: max-content;
     p {
        text-transform: uppercase;
        color: $text-color;
        margin: 0;
        text-align: left;
        margin: 0 15px;
    }

}
    .buttons {
        display: flex;
        margin: 15px 15px;
        width: inherit;
        button {
            width: 33.3%;
            background-color: white;
            margin: 0;
            outline: none;
            border: 1px solid $btn-border-color;
            height:  40px;
            color: $active-btn-color;
            text-transform:uppercase;
            position: relative;
            &:first-child {
                border-radius: 5px 0 0 5px;
                left: 1px;
            }
            &:last-child {
                border-radius: 0 5px 5px 0;
                right: 1px;
            }
            &:hover {
                cursor: pointer;
                background-color: $btn-hover-color;
                border-color: $active-btn-color;
                z-index: 3;
            }
            &.active {
                background-color: $active-btn-color;
                border-color: $active-btn-color;
                color: white;
                z-index: 3;            
            }
           
        }
    }
   
    .transfers {
        display: flex;
        flex-direction: column;
        align-items: flex-start;
        margin: 0;
        padding: 0;
        li {
            height: 36px;
            width: 100%;
            padding: 0 15px;
            display: flex;
            justify-content: flex-start;
            align-items: center;
            position: relative;
            input {
                display: none;
            }
            &::after {
                content: "только";
                position: absolute;
                right: 15px;
                text-transform: uppercase;
                color: $active-btn-color;
                display: none;
            }
            &:hover {
                background-color: $btn-hover-color;
                label {
                    &::after {
                        border-color: $active-btn-color;
                    }
                }
                &::after {
                    display: block;
                }
            }
            label {
                position: relative;
                padding-left: 25px; 
                color: #4a4a4a;
                font-size: 13px;
                &::after {
                    content: "";
                    position: absolute;
                    left: 0;
                    top: 50%;
                    width: 19px;
                    height: 19px;
                    border: 1px solid #d2d5d6;
                    border-radius: 3px;
                    transform: translateY(-50%);
                }
                &.checked {     
                    &::after {
                    border-color: $active-btn-color;
                    content: "\2713";
                    color: $active-btn-color;
                    }
                    
                }

            }
        }

    }
@media (max-width: 790px) {
    .filters {
        font-size: 10px;
        font-weight: 700;
    }
    .transfers {
        li {
            label {
                font-size: 11px;
                font-weight: 500;

            }
        }
    }
}
@media (max-width: 690px) {
    .filters{
        margin-bottom: 10px;
        padding: 10px 0;

    }
    .transfers {
        flex-direction: row;
        margin-top: 10px;
        li {
            display: inline-flex;
            align-items: flex-end;
            label {
                padding-bottom: 8px;
                height: 100%;
                display: flex;
                align-items: flex-end;
            }
            &::after {
                font-size: 8px;
                position: absolute;
                right: 0;
                top: 0;
                text-transform: uppercase;
                color: $active-btn-color;
                display: none;
            }
        }
    }
}
@media (max-width: 558px) {
     .transfers {
        flex-direction: row;
        margin-top: 10px;
        li {
            padding: 0 8px;
            width: max-content;
            label {
                &::after {
                    width: 16px;
                    height: 16px;
                }
            }
           
        }
    }
}
@media (max-width: 480px) {
    .transfers {
        flex-direction: column;
        align-items: flex-start;
        margin: 0;
        padding: 0;
        li {
            width: 100%;
        }
    }
}

</style>