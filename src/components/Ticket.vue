<template>
    <li>
        <div>
            <img src="../images/Logo.svg">
            <button>Купить за {{ticket.price}} </button>
        </div>
        <div>
            <div class="time">
                <p>{{ticket.departure_time}}</p>
                <div>
                    <span v-if="ticket.stops == 1">{{ticket.stops}} пересадака</span>
                    <span v-else-if="ticket.stops == 0"></span>
                    <span v-else>{{ticket.stops}} пересадаки</span>
                     <svg width="13" height="13" viewBox="0 0 13 13" fill="none" xmlns="http://www.w3.org/2000/svg">
                        <path d="M3.9 13H5.2L8.45 7.52632L12.025 7.52632C12.5645 7.52632 13 7.06789 13 6.5C13 5.93211 12.5645 5.47368 12.025 5.47368L8.45 5.47368L5.2 0L3.9 0L5.525 5.47368H1.95L0.975 4.10526L0 4.10526L0.65 6.5L0 8.89474H0.975L1.95 7.52632H5.525L3.9 13Z" fill="#D2D5D6"/>
                    </svg>
                </div> 
                <p>{{ticket.arrival_time}}</p> 
            </div>
            <div class="date">
                <div>
                    <span>{{ticket.origin}}
                        <p>{{ticket.origin_name}}</p>
                    </span>        
                    <span>{{ticket.departure_date}}</span>
                </div>
                 <div>
                    <span>{{ticket.destination_name}}
                        <p>{{ticket.destination}}</p>
                    </span>
                   
                    <span>{{ticket.arrival_date}}</span>
                </div>
                
            </div>
        </div>

    </li>
    
</template>

<script >

    export default {
        props: {
            ticket: Object
        },
   
    }
    
</script>

<style scoped lang="scss">
$btn-background-color:#ff6d00;
$btn-hover-color: #ff8124;
li {
    display: flex;
    margin-bottom: 20px;
    background-color: white;
    box-shadow: 0px 1px 4px 0px rgba(91,137,164,0.25);
    border-radius: 5px;
    & > div{
        padding: 25px 20px;

        &:first-child {
            width: 36%;
            border-right: 1px solid  #eceff1;
            button {
                box-shadow: 0px 2px 1px 0px rgba(0,0,0,0.1);
                box-shadow: 0px 1px 0px 0px #d64d08;
                width: 160px;
                height: 56px;
                background-color: $btn-background-color;
                color: white;
                font-size: 16px;
                font-weight: 400;
                border-radius: 5px;
                border: none;
                &:hover {
                    cursor: pointer;
                    background-color: $btn-hover-color;
                    box-shadow: 0px 1px 5px 0px rgba(0,0,0,0.25);
                    box-shadow: 0px 1px 0px 0px #f7661d;
                }
            }

        }
        &:last-child {
            width: 64%;
            .time {
                display: flex;
                justify-content: space-between;
                p {
                    display: inline-block;
                    margin: 0;
                    font-size: 32px;
                    font-weight: 400;
                    color: #4a4a4a;
                }
                div {
                    font-size: 10px;
                    min-width: 96px;
                    color: #8b9497;
                    font-weight: 400;
                    position: relative;
                    border-bottom: 1px solid #d2d5d6;
                    height: min-content;
                    text-transform: uppercase;
                    padding: 5px 15px;
                    svg {
                        position: absolute;
                        right: 0;
                        bottom: 0;
                        transform: translate(100%, 50%);
                    }
                }
            }
            .date {
                display: flex;
                justify-content: space-between;
                div {
                    text-align: left;
                    span {
                        display: block;
                        font-size: 12px;
                        color: #4a4a4a;
                        font-weight: 400;
                        p {
                            display: inline-block;
                            margin: 0;
                        }
                        &:last-child{
                            color:#8b9497;
                        }
                    }
                    &:last-child {
                        text-align:right;
                    }
                }
            }
        }
    }
}

</style>