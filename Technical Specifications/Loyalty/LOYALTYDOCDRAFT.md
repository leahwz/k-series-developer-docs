
# 3rd Party Loyalty Integration


## Setup

In order for you to start testing, you will need to provide us with an endpoint to which we can send the contents of the scanned QR Code.

We advise two different endpoints, however, it is possible with only one as well. In that case and at the moment of the scan, a query parameter needs to be set up with the value “code”.


## Process


### Method

POST


### Scan the foreign QR

Upon scanning a foreign QR code will identify it and hit your endpoint with the decoded value of the QR Code and the following query string parameters



* **Code:** is the QR Code contents
* **businessId:** is the iKentoo business identifier. A business can contain multiple business locations
* **businessLocationId:** is the site identifier for this business
* **tillId:** is the ID if the POS which scanned the QR Code


### Respond

Once the information is sent to your endpoint, your system will need to process the hit as quickly as possible (this directly impacts the customer experience at the POS) and return the following JSON in the request.


```
{
"externalReference": {
		"prefix": "NAVTECH",
		"reference": "REF123 - i - am - unique"
	},
	"displayMessage": "You Win",
	"consumer": {
		"firstName": "Serge",
		"lastName": "Sozonoff",
		"companyName": null,
		"phoneNumber1": null,
		"emailAddress": "serge@ikentoo.com",
		"consumerNotes": null,
		"thirdPartyConsumerReference": null
	},
	"rewardBasket": {
		"discountCode": "10PCT",
		"productRewardList": [{
			"sku": "CKE",
			"price": null,
			"discountCode": null,
			"modifyItemIfFound": false
		}, {
			"sku": "SKU123",
			"price": null,
			"discountCode": "10PCT",
			"modifyItemIfFound": true
		}, {
			"sku": "OD1",
			"price": 10000,
			"discountCode": null,
			"modifyItemIfFound": false
		}]
	}
}
```


<span style="text-decoration:underline;">Important - Definitions</span>



* In thirdPartyConsumerReference, you can put the “member ID"
* Reward basked is optional
* rewardBasket contains rewards applied to the current transaction.
* externalReference is attached to the transaction (if the transaction is completed). You or the client can use this to reconcile with the financial data.
* displayMessage is show on the POS display as a modal view
* consumer contains consumer info
* top level discountCode is a discount applied to the who account/purchase
* productRewardList: the list of items available for the reward

most of those fields should be self-explanatory except for:


```
modifyItemIfFound
      {
    "sku": "SKU123",
    "price": null,
    "discountCode": "10PCT",
     "modifyItemIfFound": true
}
```


In the above example, if SKU123 is found in the basket we will apply the discount with the code 10PCT to a single line with that SKU. If it’s not found we will first add it and then apply the discount.

If modifyItemIfFound is false then we will not attempt to modify an existing item but we will ALWAYS add a new one with the discount if specified.


### Matching of the basket and the consumer

You can respond with either the externalReference or the thirdPartyConsumerReference or both if needed. Thus on account close, you'll have that information in the payload.

You can also respond with a discount and/or a product reward list and/or a displayMessage that will appear on the POS.


## Example response payload in the callback in accountClose


```
{
  "notificationType": "UPDATE",
  "account": {
    "id": 85474144161502,
    "uuid": null,
    "businessLocationId": 9148280340482,
    "name": "Order 2",
    "accountNumber": "A4975.244",
    "currencyCode": "EUR",
    "deviceId": 4975,
    "deviceName": "iPad84",
    "deviceIp": null,
    "staffId": 1251,
    "staffName": "Manager",
    "staffEmail": null,
    "openDate": 1553609526916,
    "closeDate": 1553609597693,
    "paidAmount": 9.5,
    "totalAmount": 9.5,
    "coverCount": 0,
    "gratuityAmount": 0,
    "receiptNumber": "R4975.62",
    "cancelled": false,
    "accountProfileCode": "DIRECTE",
    "transactionLines": [
      {
        "id": 85474144161503,
        "parentLineId": null,
        "accountId": 85474144161502,
        "currencyCode": null,
        "amount": 3.5,
        "unitAmount": 3.5,
        "quantity": 1,
        "staffId": 1251,
        "staffName": "Manager",
        "staffEmail": null,
        "nameOverride": "",
        "itemDescription": "Expresso",
        "accountingGroupId": "9148280340523",
        "accountingGroupName": "Boissons",
        "itemId": 9148280340801,
        "itemSku": "44",
        "date": 1553609576963,
        "active": true,
        "deviceId": 4975,
        "deviceName": "iPad84",
        "deviceIp": null,
        "activeTax": {
          "code": "TVAR10",
          "description": "TVA 10%",
          "rate": 1.1,
          "taxIncluded": true
        },
        "subLines": [],
        "discounts": [],
        "tags": ""
      },
      {
        "id": 85474144161504,
        "parentLineId": null,
        "accountId": 85474144161502,
        "currencyCode": null,
        "amount": 6,
        "unitAmount": 6,
        "quantity": 1,
        "staffId": 1251,
        "staffName": "Manager",
        "staffEmail": null,
        "nameOverride": "",
        "itemDescription": "Chocolat chaud",
        "accountingGroupId": "9148280340523",
        "accountingGroupName": "Boissons",
        "itemId": 9148280340797,
        "itemSku": "43",
        "date": 1553609596725,
        "active": true,
        "deviceId": 4975,
        "deviceName": "iPad84",
        "deviceIp": null,
        "activeTax": {
          "code": "TVAR10",
          "description": "TVA 10%",
          "rate": 1.1,
          "taxIncluded": true
        },
        "subLines": [],
        "discounts": [],
        "tags": ""
      }
    ],
    "paymentLines": [
      {
        "id": 85474144161505,
        "accountId": 85474144161502,
        "currencyCode": "EUR",
        "gratuityAmount": 0,
        "amount": 9.5,
        "staffId": 1251,
        "staffName": "Manager",
        "staffEmail": null,
        "date": 1553609597681,
        "active": true,
        "paymentMethod": "CASH",
        "paymentMethodDescription": "Espèces",
        "deviceId": 4975,
        "deviceName": "iPad84",
        "deviceIp": null,
        "externalReference": null
      }
    ],
    "discounts": [],
    "externalReferences": [],
    "deliveryInformation": {
      "id": null,
      "enabled": true,
      "deliveryMode": "COLLECTION",
      "deliveryState": "IN_PRODUCTION",
      "collectionCode": "2",
      "deliveryInfo": "",
      "deliveryDueTime": null,
      "deliveryTime": null,
      "deliveredTime": null,
      "productionDueTime": null,
      "prepaid": false,
      "deliveryOrigin": "POS",
      "deviceName": "iPad84"
    },
    "consumerRecord": null,
    "currentProductionPhase": 0,
    "currentInsertionPhase": 0,
    "accountObjectId": null,
    "status": "closed"
  },
  "event": null,
  "retryCounter": 0,
  "businessLocationId": 9148280340482
}
```



## Authentication

At the moment we don’t have an authentication concept implemented.


## Future developments

We will also POST some JSON which will represent the current customer basket but this is not implemented yet, so for the time being you’ll receive an empty {} JSON body.
