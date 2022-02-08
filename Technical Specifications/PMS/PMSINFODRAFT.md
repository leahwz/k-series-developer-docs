# PMS Integration 

In line with our policy, PMS partners have to complete the integration according to the standards mentioned below.


## 1. GET /search

**GET /search?term=XXX, produces application/json**

This endpoint should search for a room number corresponding to the specified ‘term’ and return any matching reservation.

In case the PMS supports it, the term could be a customer name, or a part of a customer name, in which case any matching reservation should be returned as well.

The request should return a JSON object, with a flag ‘success’, and an errorMessage in case success is false, and an array of Reservation.

<span style="text-decoration:underline;">Sample:</span>

{ "success": true, "errorMessage": null, "reservations": [ ... ] }

<span style="text-decoration:underline;">Reservation array: </span>


<table>
  <tr>
   <td><strong>roomId</strong>
   </td>
   <td>String
   </td>
   <td>The room number (can be alphanumeric) i.e. 123A
   </td>
  </tr>
  <tr>
   <td><strong>roomDescription</strong>
   </td>
   <td>String
   </td>
   <td>The room description. Ex: "Room 123" or "Matterhorn Suite". If the PMS does not provide anything then add a copy of roomId
   </td>
  </tr>
  <tr>
   <td><strong>clientName</strong>
   </td>
   <td>String
   </td>
   <td>The full name of the client corresponding to that reservation i.e. "Jean Dupont"
   </td>
  </tr>
  <tr>
   <td><strong>reservationId</strong>
   </td>
   <td>String
   </td>
   <td>The reservation identifier i.e. 1234567 (there can be multiple reservations for the same room)
   </td>
  </tr>
  <tr>
   <td><strong>blocked</strong>
   </td>
   <td>Boolean
   </td>
   <td>If true, that reservation is not authorized to receive POS orders.
   </td>
  </tr>
</table>



##


## 2. POST /charge

**POST /charge consumes application/json, produces application/json**

The request body, is an **Account**, a JSON object, with the following fields:

<span style="text-decoration:underline;">Account:</span>


<table>
  <tr>
   <td><strong>apiKey</strong>
   </td>
   <td>string
   </td>
   <td>an opaque reference provided during the customer account configuration identifying iKentoo and/or the customer (basically the credentials)
   </td>
  </tr>
  <tr>
   <td><strong>businessExternalReference</strong>
   </td>
   <td>string
   </td>
   <td>an opaque reference provided during the customer account configuration
   </td>
  </tr>
  <tr>
   <td><strong>name</strong>
   </td>
   <td>string
   </td>
   <td>the account name
   </td>
  </tr>
  <tr>
   <td><strong>openDate</strong>
   </td>
   <td>iso8601 UTC date time w/o ms
   </td>
   <td>the account open date
   </td>
  </tr>
  <tr>
   <td><strong>closeDate</strong>
   </td>
   <td>iso8601 UTC date time w/o ms
   </td>
   <td>nullable
   </td>
  </tr>
  <tr>
   <td><strong>ownerId</strong>
   </td>
   <td>unsigned integer with max value 263-1
   </td>
   <td>the identifier of the account owner
   </td>
  </tr>
  <tr>
   <td><strong>ownerName</strong>
   </td>
   <td>string
   </td>
   <td>the name of the account owner
   </td>
  </tr>
  <tr>
   <td><strong>deviceId</strong>
   </td>
   <td>unsigned integer with max value 263-1
   </td>
   <td>the identifier of the till where the account was created
   </td>
  </tr>
  <tr>
   <td><strong>transactions</strong>
   </td>
   <td>array
   </td>
   <td>See below
   </td>
  </tr>
  <tr>
   <td><strong>payments</strong>
   </td>
   <td>array
   </td>
   <td>See below
   </td>
  </tr>
  <tr>
   <td><strong>paymentDate</strong>
   </td>
   <td>iso8601 UTC date time w/o ms
   </td>
   <td>the payment date
   </td>
  </tr>
  <tr>
   <td><strong>receipt</strong>
   </td>
   <td>string
   </td>
   <td>a text representation of the receipt
   </td>
  </tr>
</table>


<span style="text-decoration:underline;">Transaction array:</span>


<table>
  <tr>
   <td><strong>unitAmount</strong>
   </td>
   <td>decimal
   </td>
   <td>the amount per unit
   </td>
  </tr>
  <tr>
   <td><strong>amount</strong>
   </td>
   <td>decimal
   </td>
   <td>the line total amount
   </td>
  </tr>
  <tr>
   <td><strong>description</strong>
   </td>
   <td>string
   </td>
   <td>the item description / name
   </td>
  </tr>
  <tr>
   <td><strong>staffId</strong>
   </td>
   <td>unsigned integer with max value 263-1
   </td>
   <td>the identifier of the staff responsible for the line
   </td>
  </tr>
  <tr>
   <td><strong>staffName</strong>
   </td>
   <td>string
   </td>
   <td>the name of the staff responsible for the line
   </td>
  </tr>
  <tr>
   <td><strong>groupId</strong>
   </td>
   <td>unsigned integer with max value 263-1
   </td>
   <td>the identifier of the accounting group
   </td>
  </tr>
  <tr>
   <td><strong>groupName</strong>
   </td>
   <td>string
   </td>
   <td>the name of the accounting group
   </td>
  </tr>
  <tr>
   <td><strong>taxId</strong>
   </td>
   <td>unsigned integer with max value 263-1
   </td>
   <td>the identifier of the tax
   </td>
  </tr>
  <tr>
   <td><strong>taxName</strong>
   </td>
   <td>string
   </td>
   <td>the name of the tax
   </td>
  </tr>
  <tr>
   <td><strong>taxRate</strong>
   </td>
   <td>decimal
   </td>
   <td>the tax rate (+1)
   </td>
  </tr>
  <tr>
   <td><strong>taxIncluded</strong>
   </td>
   <td>boolean
   </td>
   <td>a flag indicating whether the tax is included or not
   </td>
  </tr>
</table>


<span style="text-decoration:underline;">Payment array:</span>


<table>
  <tr>
   <td><strong>staffId</strong>
   </td>
   <td>unsigned integer with max value 263-1
   </td>
   <td>the identifier of the staff responsible for the line
   </td>
  </tr>
  <tr>
   <td><strong>staffName</strong>
   </td>
   <td>string
   </td>
   <td>the name of the staff responsible for the line
   </td>
  </tr>
  <tr>
   <td><strong>amount</strong>
   </td>
   <td>decimal
   </td>
   <td>the payment amount
   </td>
  </tr>
  <tr>
   <td><strong>gratuity</strong>
   </td>
   <td>decimal
   </td>
   <td>the gratuity amount
   </td>
  </tr>
  <tr>
   <td><strong>methodCode</strong>
   </td>
   <td>string
   </td>
   <td>the payment method code
   </td>
  </tr>
  <tr>
   <td><strong>methodName</strong>
   </td>
   <td>string
   </td>
   <td>the payment method name
   </td>
  </tr>
  <tr>
   <td><strong>reservationId</strong>
   </td>
   <td>string
   </td>
   <td>the identifier of the reservation in the PMS
   </td>
  </tr>
</table>


<span style="text-decoration:underline;">Sample:</span>


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


In case the PMS supports it, the Account might contain multiple payments, assigned to different reservation.

In case the PMS supports it, the Account might contain multiple payments, some of them with a payment method that is not ‘IKPMS’, such payments should not be charged by the PMS.


## PMS Configuration

The partner can add and and configure a PMS Provider per business location using the `/pms/v1/providers/` endpoint. When a PMS Provider is created, a payment method will also be created in the POS and linked to the PMS Provider.

To access this endpoint, the **OAuth scope <code><em>propertymanagement</em></code> is required</strong>.

PMS Providers API Specification: [https://api-trial.ikentoo.com/pms/swagger-ui/index.html](https://api-trial.ikentoo.com/pms/swagger-ui/index.html)

The PMS Provider is added to the account by sending a POST request to the `/pms/v1/providers/` endpoint. Below is an example request and the description of the fields that may be supplied.


<table>
  <tr>
   <td><strong>Field</strong>
   </td>
   <td><strong>Description</strong>
   </td>
  </tr>
  <tr>
   <td>businessLocationId
   </td>
   <td>The business location ID where the PMS will be configured.
   </td>
  </tr>
  <tr>
   <td>name
   </td>
   <td>The name of the payment method.
   </td>
  </tr>
  <tr>
   <td>endpoint
   </td>
   <td>The endpoint that requests will be sent to from Lightspeed.
   </td>
  </tr>
  <tr>
   <td>apiKey
   </td>
   <td>The API key to be used in the requests.
   </td>
  </tr>
  <tr>
   <td>features
   </td>
   <td>Which special features the PMS should support. Possible options are:
<ul>

<li>SEARCH_BY_NAME

<li>MIRRORING

<li>PARTIAL_PAYMENTS

<li>MULTI_PAYMENTS
</li>
</ul>
   </td>
  </tr>
</table>


**Sample:**


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
