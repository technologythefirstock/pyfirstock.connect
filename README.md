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

```python 
from thefirstock import thefirstock

login = thefirstock.firstock_login(
    userId='',
    password='',
    DOBnPAN='',
    vendorCode='',
    appkey='',
)
```

## Logout

The API session is destroyed by this call and it invalidates the access_token. The user will be sent through a new login flow after this.
```python 
from thefirstock import thefirstock

logout = thefirstock.firstock_logout()
```

## User Details

This allows to fetch the complete information of the logged in user.
```python 
from thefirstock import thefirstock
clientDetails = thefirstock.firstock_userDetails()
```

## Place Order

The place order APIs allow you to place your orders in our system.

You will get the order confirmation instantly with order_id.

```python 
from thefirstock import thefirstock

placeOrder = thefirstock.firstock_placeOrder(
    exchange="",
    tradingSymbol="",
    quantity="",
    price="",
    product="",
    transactionType="",
    priceType="",
    retention="",
    triggerPrice="",
    remarks=""
)

```

## Order Margin

You can view the margin requirement for the selected order before placing the order.
```python 
from thefirstock import thefirstock

oM = thefirstock.firstock_orderMargin(
    exchange="",
    tradingSymbol="",
    quantity="",
    price="",
    product="",
    transactionType="",
    priceType="",
)
```

## Order Book

When an order is placed, the status of the order can be viewed in the order book (Open, Executed, canceled, rejected)

```python 
from thefirstock import thefirstock
oB = thefirstock.firstock_orderBook()
```

## Cancel Order

As long as an order is open or pending in the system, it can be canceled.

```python 
from thefirstock import thefirstock

cO = thefirstock.firstock_cancelOrder(
    norenordno=""
)
```

## Modify Order

As long as an order is open or pending in the system, certain attributes of it may be modified.
```python 
from thefirstock import thefirstock

mO = thefirstock.firstock_ModifyOrder(
    norenordno="",
    quantity="",
    triggerPrice="",
    price="",
    exchange="",
    tradingSymbol="",
    priceType=""
)
```

## Single Order History

Successful placement of an order via the API does not imply its successful execution. To know the true status of a placed order, you should retrieve the particular order's current status using its order_id.

```python 
from thefirstock import thefirstock

SOH = thefirstock.firstock_SingleOrderHistory(
    norenordno=""
)
```

## Trade Book

It provides the executed trades details for the current trading day.
```python 
from thefirstock import thefirstock
TD = thefirstock.firstock_TradeBook()
```

## Positions Book

The positions book contains the user's portfolio of short to medium-term derivatives (futures and options contracts) and intraday equity stocks. Instruments in the position’s portfolio remain there until they're sold, or until expiry. Equity positions carried overnight moves to the holding’s portfolio the next day.

```python 
from thefirstock import thefirstock
PB = thefirstock.firstock_PositionBook()
```

## Product Conversion

Position conversion is the process of converting the Intraday position to overnight and the overnight position to Intraday
```python 
from thefirstock import thefirstock

PC = thefirstock.firstock_ConvertProduct(
    exchange="",
    tradingSymbol="",
    quantity="",
    product="",
    previousProduct="",
    transactionType="",
    positionType=""
)
```

## Holdings

Holdings contain long and short-term equity delivery stocks. You will be able to see Demat Holdings, Collateral Holding, and Unsettled holding which is supposed to get delivered from the exchange.
```python 
from thefirstock import thefirstock

Hold = thefirstock.firstock_Holding()
```

## Limits

Limits contain all the details about cash available, margin used, collateral margin, pay in for the day, etc.
```python 
from thefirstock import thefirstock
limit = thefirstock.firstock_Limits()
```

## Get Quotes

The market quotes APIs enable you to retrieve market data snapshots of various instruments. These are snapshots gathered from the exchanges at the time of the request. For realtime streaming market quotes, use the WebSocket API.
```python 
from thefirstock import thefirstock

gQ = thefirstock.firstock_GetQuotes(
    exchange="",
    token=""
)
```

## Search Scripts

The Search Scripts APIs enable you to search instruments using key words.
```python 
from thefirstock import thefirstock

SS = thefirstock.firstock_SearchScrips(
    stext=""
)
```

## Get Security Info
The Get SecurityInfo APIs enable you to get comliate information about the instruments .

```python 
from thefirstock import thefirstock

SI = thefirstock.firstock_SecurityInfo(
    exchange="",
    token=""
)
```

## Get Index List

The Get Index List APIs enable you to find all index name and sript code for getting index value.
```python 
from thefirstock import thefirstock

IL = thefirstock.firstock_IndexList(
    exchange=""
)
```

## Get Option Chain

The Get Option Chain APIs enable you to find all option scrip code for the usderlaying instrument.

using scrip code you can subscrib for websocket data
```python 
from thefirstock import thefirstock

OC = thefirstock.firstock_OptionChain(
    tradingSymbol="",
    exchange="",
    strikePrice="",
    count=""
)
```

## Span Calculator

The Span Calculator APIs enable you to calculate margin requirement for the posrfolio before placing order.
```python 
from thefirstock import thefirstock

SP = thefirstock.firstock_SpanCalculator(
    exchange="",
    instname="",
    symbolName="",
    expd="",
    optt="",
    strikePrice="",
    netQuantity="",
    buyQuantity="",
    sellQuantity=""
)
```

## Time Price Series
The Get Time Price Data APIs enable you to get chart data for analysis.
```python 
from thefirstock import thefirstock


TPS = thefirstock.firstock_TimePriceSeries(
    exchange="",
    token="",
    endTime="",
    startTime=""
)
```

## Websockets

## General Guidelines
The WebSocket API uses WebSocket protocol to establish a single long standing TCP connection after an HTTP handshake to receive streaming quotes. The WebSocket API is the most efficient way to receive quotes for instruments across all exchanges during live market hours.

In addition to market data, alerts, and order updates are also streamed. To connect to the Firstock WebSocket API, you will need a WebSocket client library in your choice of programming language.

Connect to 
```
wss://norenapi.thefirstock.com/NorenWSTP/
```

Keep It in Mind

(1) As soon as connection is done, a connection request should be sent with User id and login session id.  

(2) All input and output messages will be in json format.  

## Subscribe Touchline

Websocket TouchLine subscription API will provide multiple instruments available actions and possible values at once.
```python 
from typing import Any
from thefirstock import thefirstock
from thefirstock.pyClient.websocket import WsClient
from thefirstock.pyClient.websocket.enums import MessageTopic


client = thefirstock.webSocketLogin()
ws = client.ws


@ws.on_connect
def connected(client, message):
    if message.get('s') == 'OK':
        client.subscribe_touchline('NSE', '22')


@ws.on_message(MessageTopic.TOUCHLINE_FEED)
def msg_handler(client: WsClient, message: Any):
    print(message)


ws.connect(uid='SR1598', actid='SR1598')
ws.run_forever()

```

## Unsubscribe Touchline

```python 
from typing import Any
from thefirstock import thefirstock
from thefirstock.pyClient.websocket import WsClient
from thefirstock.pyClient.websocket.enums import MessageTopic


client = thefirstock.webSocketLogin()
ws = client.ws


@ws.on_connect
def connected(client, message):
    if message.get('s') == 'OK':
        client.unsubscribe_touchline('NSE', '22')


@ws.on_message(MessageTopic.TOUCHLINE_UNSUB)
def msg_handler(client: WsClient, message: Any):
    print(message)


ws.connect(uid='SR1598', actid='SR1598')
ws.run_forever()
```

## Subscribe Order Update

Websocket Order Status API will function in providing order status updates through websocket server connection and provide Order responses similar to the one received in Postback/Webhook.
```python 
from typing import Any
from thefirstock import thefirstock
from thefirstock.pyClient.websocket import WsClient
from thefirstock.pyClient.websocket.enums import MessageTopic


client = thefirstock.webSocketLogin()
ws = client.ws


@ws.on_connect
def connected(client, message):
    if message.get('s') == 'OK':
        client.subscribe_order('PP1583')


@ws.on_message(MessageTopic.ORDER_FEED)
def msg_handler(client: WsClient, message: Any):
    print(message)


ws.connect(uid='PP1583', actid='PP1583')
ws.run_forever()

```

## Unsubscribe Order Update

```python 
from typing import Any
from thefirstock import thefirstock
from thefirstock.pyClient.websocket import WsClient
from thefirstock.pyClient.websocket.enums import MessageTopic


client = thefirstock.webSocketLogin()
ws = client.ws


@ws.on_connect
def connected(client, message):
    if message.get('s') == 'OK':
        client.unsubscribe_order('NSE', '22')


@ws.on_message(MessageTopic.ORDER_UNSUB)
def msg_handler(client: WsClient, message: Any):
    print(message)


ws.connect(uid='SR1598', actid='SR1598')
ws.run_forever()

```

## Subscribe Depth

Websocket TouchLine subscription API will provide multiple instruments available actions and possible values at once.
```python 
from typing import Any
from thefirstock import thefirstock
from thefirstock.pyClient.websocket import WsClient
from thefirstock.pyClient.websocket.enums import MessageTopic


client = thefirstock.webSocketLogin()
ws = client.ws


@ws.on_connect
def connected(client, message):
    if message.get('s') == 'OK':
        client.subscribe_depth('PP1583')


@ws.on_message(MessageTopic.DEPTH_FEED)
def msg_handler(client: WsClient, message: Any):
    print(message)


ws.connect(uid='SR1598', actid='SR1598')
ws.run_forever()
```

## Unsubscribe Depth

Websocket TouchLine subscription API will provide multiple instruments available actions and possible values at once.
```python 
from typing import Any
from thefirstock import thefirstock
from thefirstock.pyClient.websocket import WsClient
from thefirstock.pyClient.websocket.enums import MessageTopic


client = thefirstock.webSocketLogin()
ws = client.ws


@ws.on_connect
def connected(client, message):
    if message.get('s') == 'OK':
        client.unsubscribe_depth('NSE', '22')


@ws.on_message(MessageTopic.DEPTH_UNSUB)
def msg_handler(client: WsClient, message: Any):
    print(message)


ws.connect(uid='SR1598', actid='SR1598')
ws.run_forever()
```




## Contributing
Pull requests are welcome. For major changes, please open an issue first to discuss what you would like to change.

Please make sure to update tests as appropriate.

## License
[MIT](https://choosealicense.com/licenses/mit/)
