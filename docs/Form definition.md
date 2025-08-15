# Form definition

## Options:

### label

Name of form.

### allowed_sites
Defines a list of countries (country codes) that are allowed to use this form.

### endpoint

Defines endpoint used for sending data.

### block_submit_on_start

If set to TRUE, submit button will be disabled when form is rendering.

### fields

Field list for this form.

### block_configuration_fields

Extra fields defined in block configuration - send as hidden fields (not visible on form page).

## Example:

```
label: Credit
allowed_sites:
  - dk
  - no
  - lt
  - lv
  - ee
endpoint: 'cardApplicationCase'
block_submit_on_start: TRUE
fields:
  orderCaseSubject:
    required: TRUE
    default_value: 'Credit'
  customerBusinessUnit:
    required: TRUE
  customerCustomerType:
    required: TRUE
  companyCompanyNumber:
    required: TRUE
    visibility:
      ':input[data-id="customerCustomerType"]': { value: B2B }
  orderCasePersonNumber:
    required: TRUE
    visibility:
      ':input[data-id="customerCustomerType"]': { value: B2C }
  orderCaseContactRef:
    required: TRUE
  customerTopic:
    required: TRUE
    label: 'What is the inquiry about'
    values:
      Cred_001: 'Request change of payment days'
      Cred_002: 'Request change of billing cycle'
      Cred_004: 'Review balance'
      Cred_005: 'Increase credit limit'
      Cred_006: 'Decrease credit limit'
      Cred_007: 'Other questions'
    icons:
      Cred_001: 186
      Cred_002: 152
      Cred_004: 151
      Cred_005: 157
      Cred_006: 157
      Cred_007: 174
  orderCaseValueChain:
    required: TRUE
    label: "For which type account do you want to place your inquiry for?"
    visibility:
      ':input[data-id="customerTopic"]':
        - { value: Cred_001 }
        - or
        - { value: Cred_002 }
        - or
        - { value: Cred_004 }
  orderCasePaymentTermType:
    required: TRUE
    visibility:
      ':input[data-id="customerTopic"]': { value: Cred_001 }
  orderCasePaymentDays:
    required: TRUE
    visibility:
      ':input[data-id="customerTopic"]': { value: Cred_001 }
  orderCaseBillingCycle:
    required: TRUE
    values:
      'Monthly': 'Monthly'
      'Twice a month': 'Twice a month'
      'Daily': 'Daily'
    visibility:
      ':input[data-id="customerTopic"]': { value: Cred_002 }
  orderCaseCreditLimitIncrease:
    required: TRUE
    visibility:
      ':input[data-id="customerTopic"]': { value: Cred_005 }
  orderCaseCreditLimitDecrease:
    required: TRUE
    visibility:
      ':input[data-id="customerTopic"]': { value: Cred_006 }
  orderCaseDesiredPrepaidIncrease:
    required: FALSE
    type: hidden
  orderCaseDescription:
    required: TRUE
    visibility:
      ':input[data-id="customerTopic"]': { value: Cred_007 }
block_configuration_fields:
  leadFormName:
    required: TRUE
    label: 'Define value for leadFormName field'
    help_text: 'It will be sent to Salesforce as hidden field.'
    type: textfield
```
