Accounts and Receipts
===============

**Accounts** and **Receipts** are separate but complementary records of order activity in the K-Series back office. A receipt will always have a corresponding account but an account may not always be converted into a receipt.

---

An **Account** represents an order that has been sent to the kitchen, regardless of whether it has been completed.


* Accounts are referenced by the `"ikaccountId"` field in the Order and Pay API.
  * e.g. `"ikaccountId": "A51524.1"`

* Accounts are referenced by the `"accountFiscId"` and `"initialAccountId"` fields in the Financial API.

  * e.g. `"accountFiscId": "A51524.1"`

<br>


A **Receipt** is created when the order is printed.

* Receipts are referenced by the `"receiptId"` field in the Financial API.
  * e.g. `"receiptId": "R51524.1"`


*Note: When a receipt has been printed but the order has not yet been completed, we call this a **Draft Receipt**.*




For more details on Account and Receipt reporting see the [Product Documentation](https://k-series-support.lightspeedhq.com/hc/en-us/articles/4403189420187-About-Account-Reports).
