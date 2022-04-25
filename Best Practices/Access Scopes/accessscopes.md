Access Scopes
==============

An OAuth access token can have a variety of permission levels for access to data in an account. This is called the scope. When [requesting a token](https://redoc.lsk.lightspeed.app/#section/Authentication) using your K-Series OAuth client, you will only be able to request the specific access scopes required by your integration.

During the authorization flow, the user must approve each scope individually.

### Example:

![Scopes](https://lsapi.pw/oauth/consent.png)

See the below table for the full list of access scopes:


| Scope                | Description                                                                                                           |
| -------------------- | --------------------------------------------------------------------------------------------------------------------- |
| `orders-api`         | Read business information, floors, menus, discounts, and production instructions. Read and write orders and payments. |
| `financial-api`      | Read financial data.                                                                                                  |
| `reservations-api`   | Read and write webhooks. Update Reservation statuses. Configure reservation integrations.                             |
| `items`              | Read and write items. Read rich items.                                                                                |
| `propertymanagement` | Read and write Property Management System configurations.                                                             |
