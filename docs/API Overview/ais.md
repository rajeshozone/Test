# AISP API Overview

## Base URL
The base URL for all AIS APIs is: `https://rs1.{prod_domain_name}/open-banking/v3.1/aisp/**`

## Account Access Consents
[Account Access Consents API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Account_Access)

## Accounts
[Accounts API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Accounts)

Zopa members will have one or more of the following accounts:
- Zopa Personal Account
- Zopa Personal Savings Pot
- Zopa Joint Account
- Zopa Joint Savings Pot
- Zopa Business Current Account
- Zopa Business Savings Pot

## Balances
[Balances API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Balances)

Balances shown in this endpoint provide the `InterimAvailable` value.

`InterimAvailable` balance is the value displayed most widely to our members within the Zopa apps.
-
-## Transactions
-[Transactions API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Transactions)
-
-Pagination is supported on GET /accounts/{AccountId}/transactions end point with a page size of 100 transactions.
-
-> Please note GET /transactions end point is not supported
-
-## Beneficiaries
-[Beneficiaries API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Beneficiaries)
-
-> Not currently supported.
-
-## Direct Debits
-[Direct Debits API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Direct_Debits)
-
-> Not currently supported.
-## Standing Orders
-[Standing Orders API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Standing_Orders)
-
-> Not currently supported.
-## Products
-[Products API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Products)
-
-> Not currently supported.
-
-## Offers
-[Offers API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Offers)
-
-> Not currently supported.
-## Parties
-[Parties API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Parties)
-
-> Not currently supported.
-## Scheduled Payments
-[Scheduled Payments API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Scheduled_Payments)
-
-> Not currently supported.
-## Statements
-[Statements API](/perry/developer/documentation?resource=dev-ui-portal&document=swagger/account-info-openapi.yaml#operations-tag-Statements)
-
-> Not currently supported.
