# PMS Integration

In line with our policy, PMS partners have to complete the integration according to the standards outlined below.


## 1. GET /search

##### Query Parameter: /search?term=*searchterm*

##### Produces: application/json

This endpoint should search for a room number corresponding to the specified `term` and return any matching reservation.

In case the PMS supports it, the term could be a customer name, or a part of a customer name, in which case any matching reservation should be returned as well.

The request should return a JSON object, with a `success` flag, and an errorMessage when success is `false`, as well as a `reservation` array .

##### Sample:

```
{ "success": true, "errorMessage": null, "reservations": [ ... ] }
```

#### Reservation array:


|Parameter|Datatype|Description|
|--- |--- |--- |
|**roomId**|String|The room number (can be alphanumeric) i.e. 123A|
|**roomDescription**|String|The room description. Ex: "Room 123" or "Matterhorn Suite". If the PMS does not provide anything then add a copy of roomId|
|**clientName**|String|The full name of the client corresponding to that reservation i.e. "Jean Dupont"|
|**reservationId**|String|The reservation identifier i.e. 1234567 (there can be multiple reservations for the same room)|
|**blocked**|Boolean|If true, that reservation is not authorized to receive POS orders.|




## 2. POST /charge

##### Consumes: application/json,
##### Produces: application/json

The request body, is an `Account`. A JSON object, with the following fields:

#### Account:

|Parameter|Datatype|Description|
|--- |--- |--- |
|**apiKey**|string|An reference provided during the customer account configuration (esentially, the credentials)|
|**businessExternalReference**|string|A reference provided during the customer account configuration|
|**name**|string|The account name|
|**openDate**|iso8601 UTC date time (without ms) ms|The account open date|
|**closeDate**|iso8601 UTC date time (without ms)|Nullable|
|**ownerId**|unsigned integer with max value 263-1|the identifier of the account owner|
|**ownerName**|string|The name of the account owner|
|**deviceId**|unsigned integer with max value 263-1|The identifier of the till where the account was created|
|**transactions**|array|See below|
|**payments**|array|See below|
|**paymentDate**|iso8601 UTC date time (without ms)|the payment date|
|**receipt**|string|a text representation of the receipt|


#### Transaction array:


|Parameter|Datatype|Description|
|--- |--- |--- |
|**unitAmount**|decimal|the amount per unit|
|**amount**|decimal|the line total amount|
|**description**|string|the item description / name|
|**staffId**|unsigned integer with max value 263-1|the identifier of the staff responsible for the line|
|**staffName**|string|the name of the staff responsible for the line|
|**groupId**|unsigned integer with max value 263-1|the identifier of the accounting group|
|**groupName**|string|the name of the accounting group|
|**taxId**|unsigned integer with max value 263-1|the identifier of the tax|
|**taxName**|string|the name of the tax|
|**taxRate**|decimal|the tax rate (+1)|
|**taxIncluded**|boolean|a flag indicating whether the tax is included or not|


#### Payment array:


|Parameter|Datatype|Description|
|--- |--- |--- |
|**staffId**|unsigned integer with max value 263-1|the identifier of the staff responsible for the line|
|**staffName**|string|the name of the staff responsible for the line|
|**amount**|decimal|the payment amount|
|**gratuity**|decimal|the gratuity amount|
|**methodCode**|string|the payment method code|
|**methodName**|string|the payment method name|
|**reservationId**|string|the identifier of the reservation in the PMS|

##### Sample:


```
{
"apiKey": "xyz",
"businessExternalReference": "abc",
"name": "Account name",
 "openDate": "2016-01-13T06:00:00",
"closeDate": "2016-01-13T08:00:00",
"covers": 2,
"ownerId": 3453,
"ownerName": "Ben",
"deviceId": 1122,
"transactions": [{
    "unitAmount": 100,
    "quantity": 1,
    "amount": 100,
    "description": "Coca",
    "staffId": 123,
    "staffName": "John",
    "groupId": "987938217632",
    "groupName": "Soft drinks",
    "taxId": "312312312321",
    "taxName": "VAT 20%",
    "taxRate": 1.20,
    "taxIncluded": false
    },  {
    "unitAmount": -0.12,
    "quantity": 1,
    "amount": -0.12,
    "description": "Discount 10%",
    "staffId": 123,
    "staffName": "John",
    "groupId": "987938217632",
    "groupName": "Soft drinks",
    "taxId": "312312312321",
    "taxName": "VAT 20%",
    "taxRate": 1.20,
    "taxIncluded": false
    }
   ],
"payments": [{
"paymentDate": "2016-01-13T08:00:00",
"staffId": 123,
"staffName": "John",
"amount": 1.08,
"gratuity": 0,
"methodCode": "IKPMS",
"methodName": "Room charge",
"reservationId": "1234ABC"
}
   ],
    "receipt": "Receipt in text"
}
```


In case the PMS supports it, the Account might contain multiple payments, assigned to different reservations.

In case the PMS supports it, the Account might contain multiple payments, some of them with a payment method that is not ‘IKPMS’, such payments should not be charged by the PMS.


## PMS Configuration

The partner can add and and configure a PMS Provider per business location using the `/pms/v1/providers/` [endpoint](https://redoc.lsk.lightspeed.app/#tag/PMS). When a PMS Provider is created, a payment method will also be created in the POS and linked to the PMS Provider.

To access this endpoint, the [OAuth scope](https://redoc.lsk.lightspeed.app/#section/Authentication) `propertymanagement` is required.

The PMS Provider is added to the account by sending a POST request to the `/pms/v1/providers/` endpoint. Below is an example request and the description of the fields that may be supplied.

|Field|Description|
|--- |--- |
|**businessLocationId**|The business location ID where the PMS will be configured.|
|**name**|The name of the payment method.|
|**endpoint**|The endpoint that requests will be sent to from Lightspeed.|
|**apiKey**|The API key to be used in the requests.|
|**features**|Special features the PMS supports. Possible options are: `SEARCH_BY_NAME`,`MIRRORING`, `PARTIAL_PAYMENTS`, `MULTI_PAYMENTS`|


##### Sample: 


```
POST /pms/v1/providers/
{
  "businessLocationId": 123,
  "name": "Test PMS",
  "endpoint": "https://testpms.com/restaurant",
  "apiKey": "abc2-1dsaf-34gds-124tf",
  "features": [
    "SEARCH_BY_NAME", "MIRRORING", "PARTIAL_PAYMENTS", "MULTI_PAYMENTS"
  ]
}
