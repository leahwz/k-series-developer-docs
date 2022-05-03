GetCheck
===============

The [getCheck](https://redoc.lsk.lightspeed.app/#operation/getCheck
) endpoint returns all open dine-in receipts for the current day.

It has a couple of caveats:

* It does not return receipts on accounts in Trial Mode. This is because Trial Mode does not write receipts to the financial backend.

* It will only return receipts created within the past 15 hours. Any still-open receipts more than 15 hours old will not be returned.
