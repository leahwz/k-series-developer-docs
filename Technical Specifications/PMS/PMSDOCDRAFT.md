# API Integration Guide

### Property Management System

__________________________________

### Lightspeed Hospitality K Series allows for third-partyPMS providers to integrate using the

### pms-providers API and the ‘Charge to Room’ paymentmethod. Once the integration has

### been configured and mapped to a payment method, theuser is able to send room charge

### requests to an external PMS.

## Authentication

PMS integrations require access to the OAuth scopepropertymanagement. OAuth scopes apply

to an OAuth client and are set by Lightspeed whencreating the client. More about authentication
here.

## Configuring the PMS

The first step in the setup process is to configurethe PMS via the API using thecreate PMS provider
endpoint. The partner must send a POST request toLightspeed to configure the URL that will be
called when the user selects the ‘Charge to Room’payment method.

```
businessLocationID The unique identifier of the restaurant
```
```
name The name of the PMS provider
```
```
endpoint The base URL of the PMS
```
```
apiKey The API key to be used for authentication. Is
passed as the query parameterapiKey.
```
```
features* SEARCH_BY_NAME - Allow searching by guest
name
MIRRORING -Send all receipts to the PMS
PARTIAL_PAYMENTS - Allow room charges less
than the receipt total
MULTI_PAYMENTS - Allow for multiple room
charges on the same receipt
```
_* features are not supported in the current versionof Lightspeed_

## Creating the Payment Method

Once the PMS provider has been configured, a new paymentmethod must be created in the
backoffice.


1. Navigate to thebackofficeand log in
2. Go to Configuration > Settings > Payment Methods
3. Click+Add a payment method
4. Select the payment method type:Charge to Room
5. Assign the payment type a name and accounting reference(optional)
    a. Important: the code must remain IKPMS
6. Set the PMS Server toOther
7. Save the payment method

## Add the Payment Method to a Configuration

Finally, the payment method must be added to a deviceconfiguration for it to be accessible in the app.
Go to Configuration > Configurations and edit a configuration.Scroll down to Payment methods to
allow and ensure that the newly created payment methodis highlighted. Reload the configuration on
a device to begin using the charge to room paymentmethod.


## Using the PMS

The two main functions of the PMS are guest lookupand charging a bill to a room. Requests will
always be sent to the URL that has been configuredby the partner. Lightspeed will pass the API key

that was configured by the partner as a query parameterwhen querying the PMS.

### Searching for a Guest

The first request that gets executed is the /searchrequest. Lightspeed will pass a number of query
parameters to the PMS, including the terms that theuser searched for. An array of guests matching

the terms should be returned to Lightspeed.

```
Parameter Description
```
```
term The search term entered by the end user
```
```
businessExternalReference The external reference ID assigned to the restaurant
```
```
apiKey The API key configured by the partner for the restaurant
```
Example response:
{
"success":"true",
"errorMessage":"",
"reservations":[
{
"roomId":"1002",
"roomDescription":"Room 1002",
"clientName":"Mike Test",
"reservationId":"001",
"blocked":"false"
}
]
}

### Charge Request

Lightspeed will send a POST request to the /chargeendpoint with the full receipt in the payload. In
this request, the API key is passed in the requestbody along with the receipt information.

**Example Request:**


#### POST

/pms/kseries.php/charge
User-Agent: Apache-HttpClient/4.5.2 (Java/1.8.0_131)
Content-Type:
Accept: application/json, application/*+json

{
"name":"",
"openDate":"2021-02-03T17:52:18.201Z",
"closeDate":"2021-02-03T17:53:20.034Z",
"covers":0,
"ownerId":3696,
"ownerName":"Manager",
"deviceId":12787,
"transactions":[
{
"unitAmount":2.6,
"quantity":1,
"amount":2.6,
"description":"Flat White",
"staffId":3696,
"staffName":"Manager",
"groupId":31241592111265,
"groupName":"Hot Drinks",
"taxId":31241592111109,
"taxName":"13% HST",
"taxRate":1.13,
"taxIncluded":false,
"sku":"EN18"
},
{
"unitAmount":3,
"quantity":1,
"amount":3,
"description":"Mocha",
"staffId":3696,
"staffName":"Manager",
"groupId":31241592111265,
"groupName":"Hot Drinks",
"taxId":31241592111109,
"taxName":"13% HST",
"taxRate":1.13,
"taxIncluded":false,
"sku":"EN24"


#### },

#### {

```
"unitAmount":0.73,
"quantity":1,
"amount":0.73,
"description":"Flat White",
"staffId":3696,
"staffName":"Manager",
"groupId":31241592111265,
"groupName":"Hot Drinks",
"taxId":31241592111109,
"taxName":"13% HST",
"taxRate":1.13,
"taxIncluded":false,
"sku":"EN18"
}
],
"payments":[
{
"paymentDate":"2021-02-03T17:53:20.015Z",
"staffId":3696,
"staffName":"Manager",
"gratuity":0,
"amount":6.33,
"methodName":"K Room",
"reservationId":"001",
"methodCode":"IKPMS"
}
],
"receipt":null,
"uuid":"3fWX14EFTFmeuw1IwnTiMA==",
"id":null,
"fiscId":null,

"businessExternalReference":"ls-trialdev-ef41-4a54-a6d2-0b63d787ee9d"
,
"apiKey":"4f78da63-8c65-4da4-915c-3ba859a70cfb",
"identifier":"3fWX14EFTFmeuw1IwnTiMA=="
}
```
