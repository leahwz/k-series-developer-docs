# Real Time Notifications


## Introduction

Below you will find examples of RTN payloads sent to configured webhooks.


### Examples:

***

### Notification Type: OPEN


```
{
 "notificationType": "OPEN",
 "account": {
   "id": 379610684457353,
   "uuid": null,
   "businessLocationId": 40570261078018,
   "name": "floor plan test, Table 2",
   "accountNumber": "A22096.23",
   "currencyCode": "GBP",
   "deviceId": 22096,
   "deviceName": "iPad10",
   "deviceIp": null,
   "staffId": 12025,
   "staffName": "Online Order",
   "staffEmail": null,
   "openDate": 1638473552051,
   "closeDate": null,
   "paidAmount": 0,
   "totalAmount": 10,
   "coverCount": 2,
   "gratuityAmount": 0,
   "receiptNumber": null,
   "cancelled": false,
   "accountProfileCode": "AAP",
   "transactionLines": [
     {
       "id": 379610684457354,
       "parentLineId": null,
       "accountId": 379610684457353,
       "currencyCode": null,
       "amount": 10,
       "unitAmount": 10,
       "quantity": 1,
       "staffId": 12025,
       "staffName": "Online Order",
       "staffEmail": null,
       "nameOverride": "",
       "itemDescription": "burger",
       "accountingGroupId": "40570261078059",
       "accountingGroupName": "Food",
       "itemId": 40570261078206,
       "itemSku": "19",
       "date": 1638473552052,
"active": true,
       "deviceId": 22096,
       "deviceName": "iPad10",
       "deviceIp": null,
       "activeTax": {
         "code": "VAT20",
         "description": "VAT 20%",
         "rate": 1.2,
         "taxIncluded": true
       },
       "subLines": [],
       "discounts": [],
       "tags": "",
       "phase": 0,
       "categories": [
         {
           "category": "default",
           "value": ""
         }
       ]
     }
   ],
   "paymentLines": [],
   "discounts": [],
   "externalReferences": [
     {
       "prefix": "TASK",
       "reference": "OO-40570261078018-TESTtfLreaxzh"
     }
   ],
   "deliveryInformation": {
     "id": null,
     "enabled": false,
     "deliveryMode": "LOCAL",
     "deliveryState": "IN_PRODUCTION",
     "collectionCode": "",
     "deliveryInfo": null,
     "deliveryDueTime": null,
     "deliveryTime": null,
     "deliveredTime": null,
     "productionDueTime": null,
     "prepaid": false,
     "deliveryOrigin": "API",
     "deviceName": "iPad10"
   },
   "consumerRecord": {
     "id": 76943,
     "consumerRecordUUID": "9e2921d0-5cf5-4ae1-b3b4-2fa45b9ac10b",
     "consumer": {
       "id": 8061,
       "recordId": null,
       "firstSeenByBusinessId": null,
       "creationDate": null,
       "emailAddress": "test@email.com",
       "language": null,
       "ticketCount": null,
       "totalAmount": null,
       "gratuityAmount": null,
       "contactInformation": null
     },
     "contactInformation": {
       "id": null,
       "salutation": null,
       "firstName": "John",
       "lastName": "Doe",
       "companyName": "",
       "phoneNumber1": "",
       "phoneNumber2": "",
       "addressLine1": "",
       "addressLine2": "",
       "zipCode": "",
       "city": "",
       "taxIdentifier": "",
       "emailReceipts": true,
       "fullName": "John Doe"
     },
     "consumerNotes": [],
     "externalReferences": []
   },
   "currentProductionPhase": 0,
   "currentInsertionPhase": 0,
   "accountObjectId": 40570261078218,
   "paymentInProgress": false,
   "latestExternalReferences": [
     {
       "prefix": "TASK",
       "reference": "OO-40570261078018-TESTtfLreaxzh"
     }
   ],
   "taxAmount": 1.6667,
   "preTaxAmount": 8.3333,
   "serviceCharge": 0,
   "orderMode": "DIRECT",
   "tableName": "Table 2",
   "accountProfileName": "API Account Profile",
   "accountProfileId": "40570261078214",
   "originAccountId": 379610684457348,
   "originAccountNumber": "A22096.22",
   "type": "SALE",
   "updateDate": 1638473552053,
   "offset": -300,
   "totalDiscount": 0,
   "status": "open"
 },
 "event": null,
 "retryCounter": 0,
 "businessLocationId": 40570261078018
}
```



### Notification Type: UPDATE


```
{
 "notificationType": "UPDATE",
 "account": {
   "id": 379610684457348,
   "uuid": null,
   "businessLocationId": 40570261078018,
   "name": "floor plan test, Table 2",
   "accountNumber": "A22096.22",
   "currencyCode": "GBP",
   "deviceId": 22096,
   "deviceName": "iPad10",
   "deviceIp": null,
   "staffId": 12025,
   "staffName": "Online Order",
   "staffEmail": null,
   "openDate": 1638473551940,
   "closeDate": 1638473551944,
   "paidAmount": -10,
   "totalAmount": -10,
   "coverCount": -2,
   "gratuityAmount": 0,
   "receiptNumber": null,
   "cancelled": false,
   "accountProfileCode": "AAP",
   "transactionLines": [
     {
       "id": 379610684457349,
       "parentLineId": null,
       "accountId": 379610684457348,
       "currencyCode": null,
       "amount": -10,
       "unitAmount": 10,
       "quantity": -1,
       "staffId": 12025,
       "staffName": "Online Order",
       "staffEmail": null,
       "nameOverride": "",
       "itemDescription": "burger",
       "accountingGroupId": "40570261078059",
       "accountingGroupName": "Food",
       "itemId": 40570261078206,
       "itemSku": "19",
       "date": 1638473551943,
       "active": true,
       "deviceId": 22096,
       "deviceName": "iPad10",
       "deviceIp": null,
       "activeTax": {
         "code": "VAT20",
         "description": "VAT 20%",
         "rate": 1.2,
         "taxIncluded": true
       },
       "subLines": [],
       "discounts": [],
       "tags": "",
       "phase": 0,
       "categories": [
         {
           "category": "default",
           "value": ""
         }
       ]
     }
   ],
   "paymentLines": [
     {
       "id": 379610684457350,
       "accountId": 379610684457348,
       "currencyCode": "GBP",
       "gratuityAmount": 0,
       "amount": -10,
       "staffId": null,
       "staffName": null,
       "staffEmail": null,
       "date": 1638473551944,
       "active": true,
       "paymentMethod": null,
       "paymentMethodDescription": null,
       "deviceId": 22096,
       "deviceName": "iPad10",
       "deviceIp": null,
       "externalReference": null
     }
   ],
   "discounts": [],
   "externalReferences": [
     {
       "prefix": "TASK",
       "reference": "OO-40570261078018-TESTtfLreaxzh"
     }
   ],
   "deliveryInformation": {
     "id": null,
     "enabled": false,
     "deliveryMode": "LOCAL",
     "deliveryState": "IN_PRODUCTION",
     "collectionCode": "",
     "deliveryInfo": null,
     "deliveryDueTime": null,
     "deliveryTime": null,
     "deliveredTime": null,
     "productionDueTime": null,
     "prepaid": false,
     "deliveryOrigin": "API",
     "deviceName": "iPad10"
   },
   "consumerRecord": {
     "id": 76943,
     "consumerRecordUUID": "9e2921d0-5cf5-4ae1-b3b4-2fa45b9ac10b",
     "consumer": {
       "id": 8061,
       "recordId": null,
       "firstSeenByBusinessId": null,
       "creationDate": null,
       "emailAddress": "test@email.com",
       "language": null,
       "ticketCount": null,
       "totalAmount": null,
       "gratuityAmount": null,
       "contactInformation": null
     },
     "contactInformation": {
       "id": null,
       "salutation": null,
       "firstName": "John",
       "lastName": "Doe",
       "companyName": "",
       "phoneNumber1": "",
       "phoneNumber2": "",
       "addressLine1": "",
       "addressLine2": "",
       "zipCode": "",
       "city": "",
       "taxIdentifier": "",
       "emailReceipts": true,
       "fullName": "John Doe"
     },
     "consumerNotes": [],
     "externalReferences": []
   },
   "currentProductionPhase": 0,
   "currentInsertionPhase": 0,
   "accountObjectId": 40570261078218,
   "paymentInProgress": false,
   "latestExternalReferences": [
     {
       "prefix": "TASK",
       "reference": "OO-40570261078018-TESTtfLreaxzh"
     }
   ],
   "taxAmount": -1.6667,
   "preTaxAmount": -8.3333,
   "serviceCharge": 0,
   "orderMode": "DIRECT",
   "tableName": "Table 2",
   "accountProfileName": "API Account Profile",
   "accountProfileId": "40570261078214",
   "originAccountId": 379610684457338,
   "originAccountNumber": "A22096.21",
   "type": "TRANSITORY",
   "updateDate": 1638473551944,
   "offset": -300,
   "totalDiscount": 0,
   "status": "closed"
 },
 "event": null,
 "retryCounter": 0,
 "businessLocationId": 40570261078018
}
```



### **Notification Type: CLOSE**


```
{
 "notificationType": "CLOSE",
 "account": {
   "id": 379610684457348,
   "uuid": null,
   "businessLocationId": 40570261078018,
   "name": "floor plan test, Table 2",
   "accountNumber": "A22096.22",
   "currencyCode": "GBP",
   "deviceId": 22096,
   "deviceName": "iPad10",
   "deviceIp": null,
   "staffId": 12025,
   "staffName": "Online Order",
   "staffEmail": null,
   "openDate": 1638473551940,
   "closeDate": 1638473551944,
   "paidAmount": -10,
   "totalAmount": -10,
   "coverCount": -2,
   "gratuityAmount": 0,
   "receiptNumber": null,
   "cancelled": false,
   "accountProfileCode": "AAP",
   "transactionLines": [
     {
       "id": 379610684457349,
       "parentLineId": null,
       "accountId": 379610684457348,
       "currencyCode": null,
       "amount": -10,
       "unitAmount": 10,
       "quantity": -1,
       "staffId": 12025,
       "staffName": "Online Order",
       "staffEmail": null,
       "nameOverride": "",
       "itemDescription": "burger",
       "accountingGroupId": "40570261078059",
       "accountingGroupName": "Food",
       "itemId": 40570261078206,
       "itemSku": "19",
       "date": 1638473551943,
       "active": true,
       "deviceId": 22096,
       "deviceName": "iPad10",
       "deviceIp": null,
       "activeTax": {
         "code": "VAT20",
         "description": "VAT 20%",
         "rate": 1.2,
         "taxIncluded": true
       },
       "subLines": [],
       "discounts": [],
       "tags": "",
       "phase": 0,
       "categories": [
         {
           "category": "default",
           "value": ""
         }
       ]
     }
   ],
   "paymentLines": [
     {
       "id": 379610684457350,
       "accountId": 379610684457348,
       "currencyCode": "GBP",
       "gratuityAmount": 0,
       "amount": -10,
       "staffId": null,
       "staffName": null,
       "staffEmail": null,
       "date": 1638473551944,
       "active": true,
       "paymentMethod": null,
       "paymentMethodDescription": null,
       "deviceId": 22096,
       "deviceName": "iPad10",
       "deviceIp": null,
       "externalReference": null
     }
   ],
   "discounts": [],
   "externalReferences": [
     {
       "prefix": "TASK",
       "reference": "OO-40570261078018-TESTtfLreaxzh"
     }
   ],
   "deliveryInformation": {
     "id": null,
     "enabled": false,
     "deliveryMode": "LOCAL",
     "deliveryState": "IN_PRODUCTION",
     "collectionCode": "",
     "deliveryInfo": null,
     "deliveryDueTime": null,
     "deliveryTime": null,
     "deliveredTime": null,
     "productionDueTime": null,
     "prepaid": false,
     "deliveryOrigin": "API",
     "deviceName": "iPad10"
   },
   "consumerRecord": {
     "id": 76943,
     "consumerRecordUUID": "9e2921d0-5cf5-4ae1-b3b4-2fa45b9ac10b",
     "consumer": {
       "id": 8061,
       "recordId": null,
       "firstSeenByBusinessId": null,
       "creationDate": null,
       "emailAddress": "test@email.com",
       "language": null,
       "ticketCount": null,
       "totalAmount": null,
       "gratuityAmount": null,
       "contactInformation": null
     },
     "contactInformation": {
       "id": null,
       "salutation": null,
       "firstName": "John",
       "lastName": "Doe",
       "companyName": "",
       "phoneNumber1": "",
       "phoneNumber2": "",
       "addressLine1": "",
       "addressLine2": "",
       "zipCode": "",
       "city": "",
       "taxIdentifier": "",
       "emailReceipts": true,
       "fullName": "John Doe"
     },
     "consumerNotes": [],
     "externalReferences": []
   },
   "currentProductionPhase": 0,
   "currentInsertionPhase": 0,
   "accountObjectId": 40570261078218,
   "paymentInProgress": false,
   "latestExternalReferences": [
     {
       "prefix": "TASK",
       "reference": "OO-40570261078018-TESTtfLreaxzh"
     }
   ],
   "taxAmount": -1.6667,
   "preTaxAmount": -8.3333,
   "serviceCharge": 0,
   "orderMode": "DIRECT",
   "tableName": "Table 2",
   "accountProfileName": "API Account Profile",
   "accountProfileId": "40570261078214",
   "originAccountId": 379610684457338,
   "originAccountNumber": "A22096.21",
   "type": "TRANSITORY",
   "updateDate": 1638473551944,
   "offset": -300,
   "totalDiscount": 0,
   "status": "closed"
 },
 "event": null,
 "retryCounter": 0,
 "businessLocationId": 40570261078018
}
```
