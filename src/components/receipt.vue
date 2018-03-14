<template>
    <div id="receipt">
        <!-- Order Number -->
        <div class="order-number">
            <h4>Order Number</h4>
            <h4>#{{ orderNumber }}</h4>
        </div>
        <!-- /Order Number -->
        <!-- Receipt Items -->
        <ul class="receipt-items">
            <li v-for="item in items" class="receipt-item">
                <p>{{ item.name | uppercase }}</p>
                <p>${{ item.price }}</p>
            </li>
        </ul>
        <!-- /Receipt Items -->

        <!-- Add Item Test -->
        <div class="test">
            <button v-on:click="addItem('cheeseburger', 6.99)" class="btn">Add Cheeseburger - 6.99</button>
        </div>
        <!-- /Add Item Test -->

        <!-- Subtotals -->
        <ul class="subtotals">
            <li>
                <p>Items Total:</p>
                <p>${{ getItemsListTotal }}</p>
            </li>
            <li>
                <p>Sales Tax:</p>
                <p>{{ getSalesTax }}%</p>
            </li>
            <li>
                <p>Subtotal:</p>
                <p>${{ getSubTotal }}</p>
            </li>
            <li>
                <p>Discount:</p>
                <p>{{ discount }}</p>
            </li>
            <li>
                <p>Tip:</p>
                <p>({{ getTipPerc }}%) = ${{ getTipAmt }}</p>
            </li>
        </ul>
        <!-- /Subtotals -->
        <!-- Tips -->
        <div class="tips">
            <div class="tip-controls">
                <button v-on:click="addTip(0)" class="btn is-primary">0</button>
                <button v-on:click="addTip(.1)" class="btn is-primary">10%</button>
                <button v-on:click="addTip(.15)" class="btn is-primary">15%</button>
                <button v-on:click="addTip(.2)" class="btn is-primary">20%</button>
                <button v-on:click="addTip(.25)" class="btn is-primary">25%</button>
            </div>
        </div>
        <!-- /Tips -->
        <!-- Grand Total -->
        <div class="grand-total">
            <span>Total</span>
            <span>${{ getGrandTotal }}</span>
        </div>
        <!-- /Grand Total -->
        <!-- Checkout -->
        <div class="checkout">
            Place Order
        </div>
        <!-- /Checkout -->
    </div>
</template>

<script>
export default {
    name: 'receipt',
    data() {
        return {
            items: [
                {name:'chesseburger', price: 12.67},
                {name:'fries', price: 5.34},
                {name:'drink', price: 1.58},
                {name:'cheesecake', price: 4.99}
            ],
            salesTaxPerc: .025,
            tipPerc: 0,
            discount: 0,
            grandTotal: 0,
            orderNumber: 876
        }
    },
    computed: {
        getItemsListTotal: function() {
            var total = this.items.reduce(function(acc, items) {
                return acc + Number(items.price);
            }, 0);
            return total.toFixed(2);
        },
        getSubTotal: function() {
            let total = this.items.reduce(function(acc, items) {
                return acc + Number(items.price);
            }, 0);
            let taxIncluded = ((total * this.salesTaxPerc) + total).toFixed(2);
            return taxIncluded;
        },
        getSalesTax: function() {
            return (this.salesTaxPerc * 100).toFixed(1);
        },
        getTipPerc: function() {
            return this.tipPerc * 100;
        },
        getTipAmt() {
            return (this.getSubTotal * this.tipPerc).toFixed(2);
        },
        getGrandTotal() {
            return (Number(this.getTipAmt) + Number(this.getSubTotal)).toFixed(2);
        }
    },
    methods: {
        addTip(value) {
            return this.tipPerc = value;
        },
        addItem(name, price) {
            return this.items.push({ name: name, price: price });
        }
    },
    filters: {
        tip15(value) {
            return (value * .15).toFixed(2);
        },
        tip20(value) {
            return (value * .2).toFixed(2);
        },
        tip25(value) {
            return (value * .25).toFixed(2);
        },
        uppercase(value) {
            return value.charAt(0).toUpperCase() + value.slice(1);
        }
    }
}
</script>

<style>
    #receipt {
        flex: 0 0 25%;
        max-width: 500px;
        display: flex;
        flex-direction: column;
        justify-content: space-between;
        background-color: white;
    }
    #receipt p {
        margin: 0;
    }
    .order-number {
        display: flex;
        justify-content: space-between;
        padding: 1rem 2rem 1rem;
        border-bottom: 2px dashed #F4F6F8;
    }
    .order-number h4 {
        margin: 0;
    }
    .receipt-items {
        padding: 1rem 2rem;
        flex: 1 1 auto;
        overflow-y: auto;
    }
    .receipt-item {
        display: flex;
        justify-content: space-between;
    }
    .subtotals {
        padding: 1.5rem 2rem 0.5rem;
        border-top: 2px dashed #F4F6F8;
    }
    .subtotals > li {
        display: flex;
        justify-content: space-between;
    }
    .tips {
        padding: 1rem 2rem 2rem;
    }
    .tip-controls {
        display: flex;
        justify-content: space-between;
    }
    .tip-controls > button {
        flex: 1 1 auto;
        padding: 1rem 0;
        font-size: 0.8rem;
        background-color: rgb(230, 230, 230);
        color: #363636;
        font-weight: 900;
        outline: none!important;
        border: none!important;
        margin-right: 6px;
        border-radius: 3px;
    }
    .tip-controls > button:hover {
        cursor: pointer;
    }
    .tip-controls > button:active {
        background-color: rgb(190, 190, 190);
    }
    .tip-controls > button:last-child {
        margin-right: 0;
    }
    .tip-controls > button.active {
        background-color: rgb(29, 207, 163);
        color: white;
    }
    .grand-total {
        margin-top: auto;
        width: 100%;
        background-color: #3B3C3C;
        color: white;
        padding: 2rem;
        display: flex;
        justify-content: space-between;
        font-weight: 700;
        font-size: 1.7rem;
    }
    .checkout {
        padding: 2rem;
        text-align: center;
        font-weight: 700;
        font-size: 1.5rem;
        background-color: rgb(15, 190, 94);
        color: white;
        text-transform: uppercase;
    }
    .checkout:hover {
        cursor: pointer;
    }
</style>