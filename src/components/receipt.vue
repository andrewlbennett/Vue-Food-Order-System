<template>
    <div id="receipt">
        <!-- Order Number -->
        <div class="order-number">
            <h4>Order Number</h4>
            <h4>#876</h4>
        </div>
        <!-- /Order Number -->
        <!-- Receipt Items -->
        <ul class="receipt-items">
            <li v-for="item in items" class="receipt-item">
                <p>{{item.name}}</p>
                <p>${{item.price}}</p>
            </li>
        </ul>
        <!-- /Receipt Items -->
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
                <p>Discount:</p>
                <p>0%</p>
            </li>
            <li>
                <p>Tip:</p>
                <p>0%</p>
            </li>
            <li>
                <p>Subtotal:</p>
                <p>${{ getSubTotal }}</p>
            </li>
        </ul>
        <!-- /Subtotals -->
        <!-- Tips -->
        <div class="tips">
            <div class="tip-controls">
                <button class="btn is-primary active">0</button>
                <button class="btn is-primary">5%</button>
                <button class="btn is-primary">10%</button>
                <button class="btn is-primary">15%</button>
                <button class="btn is-primary">20%</button>
                <button class="btn is-primary">25%</button>
            </div>
            <!-- <p><b>15%:</b> ${{ getSubTotal | tip15 }} = ${{ getTipTotal15 }}</p>
            <p><b>20%:</b> ${{ getSubTotal | tip20 }} = ${{ getTipTotal20 }}</p>
            <p><b>25%:</b> ${{ getSubTotal | tip25 }} = ${{ getTipTotal25 }}</p> -->
        </div>
        <!-- /Tips -->
        <!-- Grand Total -->
        <div class="grand-total">
            <span>Total</span>
            <span>$45.67</span>
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
            salesTaxPerc: .025 // Sales Tax Percentage
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
        getTipTotal15: function() {
            let subTotal = this.getSubTotal;
            let tipTotal = (this.getSubTotal * .15);
            let total = (Number(tipTotal) + Number(subTotal)).toFixed(2);
            return total;
        },
        getTipTotal20: function() {
            let subTotal = this.getSubTotal;
            let tipTotal = (this.getSubTotal * .2);
            let total = (Number(tipTotal) + Number(subTotal)).toFixed(2);
            return total;
        },
        getTipTotal25: function() {
            let subTotal = this.getSubTotal;
            let tipTotal = (this.getSubTotal * .25);
            let total = (Number(tipTotal) + Number(subTotal)).toFixed(2);
            return total;
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
        border-bottom: 1px solid #DBDDDE;
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
        border-top: 1px solid #DBDDDE;
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
        padding: 0.5rem 0;
        font-size: 0.8rem;
        background-color: rgb(230, 230, 230);
        color: #363636;
        font-weight: 700;
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
        font-size: 2rem;
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
</style>