# thefirstock

thefirstock is a node js library for calling firstock apis. 
Please visit [firstock documentation website](https://connect.thefirstock.com/) for further documentation.

## Installation

Use the package manager [pip](https://pypi.org/project/pip/) to install thefirstock.

```bash
pip install thefirstock      
```

## Login

Firstock APIs allow the user authentication using the Login API. A valid Firstock Trading Account and subscription to Firstock API Services is a pre-requisite for successful authentication.

To use this Firstock API, you need an API key. Please login to your Firstock API module to get your own API Key

The login flow is as follows:

1. Navigate to the Login API endpoint: [login](https://connect.thefirstock.com/api/login)
2. After successful login, user is redirected to the redirect uri with the auth_code 
3. POST the auth_code and appIdHash (SHA-256 of api_id + app_secret) to Validate Authcode API endpoint 
4. Obtain the access_token use that for all the subsequent requests 

```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.login({
    "userId": "",
    "password": "",
    "DOBnPAN": "",
    "vendorCode": "",
    "appkey": ""
},(err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## Logout

The API session is destroyed by this call and it invalidates the access_token. The user will be sent through a new login flow after this.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.logout((err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## User Details

This allows to fetch the complete information of the logged in user.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.getUserDetails((err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## Place Order

The place order APIs allow you to place your orders in our system.

You will get the order confirmation instantly with order_id.

```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.placeOrder({
    "exchange": "",
    "tradingSymbol": "",
    "quantity": "",
    "price": "",
    "product": "",
    "transactionType": "",
    "priceType": "",
    "retention": "",
    "triggerPrice": "",
    "remarks": ""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})

```

## Order Margin

You can view the margin requirement for the selected order before placing the order.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.orderMargin({
    exchange:"",
    tradingSymbol:"",
    quantity:"",
    price:"",
    product:"",
    transactionType:"",
    priceType:"",
},(err, result)=>{
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Order Book

When an order is placed, the status of the order can be viewed in the order book (Open, Executed, canceled, rejected)

```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.orderBook((err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## Cancel Order

As long as an order is open or pending in the system, it can be canceled.

```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.cancelOrder({norenordno:""},(err, result)=>{
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Modify Order

As long as an order is open or pending in the system, certain attributes of it may be modified.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.modifyOrder({
    norenordno: "",
    price: "",
    quantity: "",
    triggerPrice: "",
    tradingSymbol:"",
    exchange:"",
    priceType:""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Single Order History

Successful placement of an order via the API does not imply its successful execution. To know the true status of a placed order, you should retrieve the particular order's current status using its order_id.

```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.singleOrderHistory({ norenordno: "" }, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Trade Book

It provides the executed trades details for the current trading day.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.tradeBook((err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## Positions Book

The positions book contains the user's portfolio of short to medium-term derivatives (futures and options contracts) and intraday equity stocks. Instruments in the position’s portfolio remain there until they're sold, or until expiry. Equity positions carried overnight moves to the holding’s portfolio the next day.

```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.positionsBook((err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## Product Conversion

Position conversion is the process of converting the Intraday position to overnight and the overnight position to Intraday
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.productConversion({
    exchange: "",
    tradingSymbol: "",
    quantity: "",
    product: "",
    previousProduct: "",
    transactionType: "",
    positionType: ""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Holdings

Holdings contain long and short-term equity delivery stocks. You will be able to see Demat Holdings, Collateral Holding, and Unsettled holding which is supposed to get delivered from the exchange.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.holdings({ product: "" }, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Limits

Limits contain all the details about cash available, margin used, collateral margin, pay in for the day, etc.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.limits((err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## Get Quotes

The market quotes APIs enable you to retrieve market data snapshots of various instruments. These are snapshots gathered from the exchanges at the time of the request. For realtime streaming market quotes, use the WebSocket API.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.getQuotes({
    exchange: "",
    token: ""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Search Scripts

The Search Scripts APIs enable you to search instruments using key words.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.searchScripts({stext:""},(err, result)=>{
    console.log("Error, ",err)
    console.log("Result: ",result)
})
```

## Get Security Info
The Get SecurityInfo APIs enable you to get comliate information about the instruments .

```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.getSecurityInfo({
    exchange: "",
    token: ""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Get Index List

The Get Index List APIs enable you to find all index name and sript code for getting index value.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.getIndexList({exchange: ""},(err, result)=>{
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Get Option Chain

The Get Option Chain APIs enable you to find all option scrip code for the usderlaying instrument.

using scrip code you can subscrib for websocket data
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.getOptionChain({
    tradingSymbol: "",
    exchange: "",
    strikePrice: "",
    count: ""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Span Calculator

The Span Calculator APIs enable you to calculate margin requirement for the posrfolio before placing order.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.spanCalculator({
    "exchange": "",
    "instname": "",
    "symbolName": "",
    "expd": "",
    "optt": "",
    "strikePrice": "",
    "netQuantity": "",
    "buyQuantity": "",
    "sellQuantity": "",
    "product": ""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```

## Time Price Series
The Get Time Price Data APIs enable you to get chart data for analysis.
```javascript 
const Firstock = require('thefirstock');

const firstock = new Firstock();

firstock.timePriceSeries({
    exchange: "",
    token: "",
    endTime: "",
    startTime: ""
}, (err, result) => {
    console.log("Error, ", err)
    console.log("Result: ", result)
})
```



## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
