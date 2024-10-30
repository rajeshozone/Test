# PISP API Overview

## Base URL
The base URL for all AIS APIs is: `https://rs1.{prod_domain_name}/open-banking/v3.1/pisp/**`

## Supported Payment Types
The Zopa API currently only supports:
- Domestic Payments
- Domestic Scheduled Payments
- Domestic Standing Orders

The Zopa API __does not__ support:
- International payments
- File & Bulk payments
- `payment-details` end-points

Payments can only be made to existing beneficiaries.

## Overview
The following apply to all domestic payment consents:

### `InstructedAmount/Amount`
- There is no MAX `InstructedAmount/Amount` mandated by Zopa API.
- 50,000 GBP is the default maximum when opening a Zopa account, but thresholds can be managed by the customer. Zopa suggest PISP notify the PSU that the same limits apply as in their Zopa app. It is possible from time to time that `domestic-payment-consents` is authorised, but the payment initiation fails due to account limits.

### `InstructedAmount/Currency`
- `InstructedAmount/Currency` must be `GBP`

### `RemittanceInformation/Reference`
`RemittanceInformation/Reference` is a mandatory field and must adhere to the following:
- Valid characters:
  - A-Z
  - a-z
  - 0-9
  - "space"
  - The characters "&", "-", ".", "/"
- Contiguous characters – user enters 6 or more valid characters but without contiguous string of at least 6 alphanumeric characters
- Must contain a contiguous string of at least 6 alphanumeric characters
- Homogeneous string – user enters 6 or more valid characters (including valid non-alphanumeric characters) - After stripping out non-alphanumeric characters the resulting string cannot consist of all the same character

The PISP may also opt to populate reference field on behalf of the PSU

### `CreditorAccount`
<!-- theme: info -->
> ### Note
>
> Domestic-payment-consents will only be authorised if the `CreditorAccount` details are that of an already existing beneficiary i.e. one the PSU has previously created in their app.
> If a consent contains recipient info that does not meet this criteria then error will be returned to the front end, the consent will remain in status `AwaitingAuthorisation` and the PSU will not be redirected.

The PISP can address this in one of two ways:
- Notify PSU that only payments to existing recipients are permitted and in the event this condition is not met Zopa will not authorise the consent and display error modal to user
- Integrate with Zopa beneficiaries API and can confirm that the recipient already exists before sending the consent to allow for a better user experience

### `LocalInstrument`
The only `LocalInstrument` supported is faster payment scheme. This field, if specified, must have the value `UK.OBIE.FPS`. If anything other than this is sent by PISP in consent payload then an error will be returned.

However, this field is not mandatory so we suggest PISP simply not include this field and Zopa will stage consent as a faster payment.

### `Account.SchemeName`
The only supported `Account.SchemeName` is `UK.OBIE.SortCodeAccountNumber` for both `DebtorAccount` and `CreditorAccount`. Any other enum provided will return error.

## Scheduled Payment dates
Payments can be made on all days including Saturdays, Sundays and Bank Holidays

## Standing Orders
- `Initiation/FirstPaymentDateTime` must be no more than 1 calendar year in advance, or PISP will be returned an error
- `Initiation/FinalPaymentDateTime` must be after Initiation/FirstPaymentDateTime by at least a calendar day, or PISP will be returned error
- `Initiation/Frequency` supported by Zopa  are:
  - `IntrvlMnthDay:01:xx`
  - `IntrvlWkDay:01:xx`
- The following fields are not supported and will return an error if specified:
  - `NumberOfPayments`
  - `RecurringPaymentDateTime`
  - `RecurringPaymentAmount`
  - `FInalPaymentAmount`


### `IntrvlMnthDay:01:xx`
The following rules apply:
- Same day every month (i.e. if made on 4th May the next payment will be made on the 4th June), however if a payment is made on either the 29th, 30th, 31st of the month and one of the months a payment is scheduled to be in has fewer days than the month of the first payment then that payment will be made on the LAST day of that month. (e.g. first payment on 30th Jan > next payment 28th Feb > next payment 30th March.
- first two digits after IntrvlMnthDay must be set at '01', indicating a one monthly interval else PISP will be returned error
- last two digits after IntrvlMnthDay are not considered or validated by Zopa  (payment will be made as per the day in FirstPaymentDateTime)

### `IntrvlWkDay:01:xx`
The following rules apply.
- Same day of the week as the first payment (i.e. if first payment is made on Friday > next payment is made on Friday the following week) - this is number of the week i.e. 1 = monday
- first two digits after IntrvlMnthWkDay must be set at '01'
- last two digits after IntrvlMnthWkDay are not taken in to account by Zopa (payment will be made as per the day in FirstPaymentDateTime)