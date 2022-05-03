Business Locations
===============

Lightspeed K-Series accounts have two different kinds of unique identifiers: **Business ID** and **Business Location ID**.

---

The **Business ID** is the is the top level identifier for the account. An account can only have one business ID.

The **Business Location ID** represents an individual restaurant location within the account. An account can have multiple business location IDs.

When using the API, you will primarily be referencing the `businessLocationId`. One notable exception is the [Rich Item API](), which references the `businessId`.
