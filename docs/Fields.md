### Field definition
A field is a .yaml file with specific structure. The structure might be very different based on the purpose of the field. However there are some common properties which every field has to have in order to use it. These are: `id` (not empty),  `type` (not empty), `api_name`, `api_object`.

There are two types of fields:
1. Submittable to Salesforce API
2. Not submittable to Salesforce API

#### Example of submittable field structure:
```
id: companyCompanyEmail
label: 'Email'
help_text:
type: email
api_name: companyEmail
api_object: company
```

Each submittable field must have `api_name` and `api_object` properties filled up. It has to correspond to its name and object it contains to. `id` of a field has to include api name and api object, for example:

If field api name is companyEmail and field api object is companyDetails then the id has to be: `companyDetailsCompanyEmail`

File name of submittable field has to include both object name and field name provided in camelCase, for example: `companyCompanyEmail.yaml` exactly the same as `ID` + `.yaml` .

#### Example of non submittable field structure:
```
id: secondOrderProduct
label: 'Product'
help_text: ''
type: connector
join_with:
  field_details:
    id: orderCaseDescription
    api_name: description
    api_object: orderCase
  separator: ';'
  render_as: select
  submit_label: 'Product'
api_name: null
api_object: null
```

Each non submittable field must have `api_name` and `api_object` properties empty - this is what makes it different from submittable field. File name of non submittable field might be anything, but it has to following some rules:
 - should start with `_` character
 - should not contain special characters except of `_`
 - it's desired to be provided with camelCase, so it's consistent with other fields.

Example of the non submittable field filename: `_termsAndConditions.yaml`.


### Field types

Here is the list of available field types. Each field type can have different set of properties.
 - radios
 - connector
 - checkbox
 - item
 - select
 - hidden
 - file
 - number
 - textfield
 - multiple_field
 - email
 - telprefix
 - textarea
 - date
 - datetime
 - grouping

### Field properties

| type                              | radios | connector | checkbox | item | select | hidden | file | number | textfield | multiple_field | email | telprefix | textarea | date | datetime | grouping |
|-----------------------------------|--------|-----------|----------|------|--------|--------|------|--------|----------|----------------|------|----------|----------|------|---------|----------|
| id                                | x      | x         | x        | x    | x      | x      | x    | x      | x        | x              | x    | x        | x        | x    | x       | x        |
| api_name                          | x      | x         | x        | x    | x      | x      | x    | x      | x        | x              | x    | x        | x        | x    | x       | x        |
| api_object                        | x      | x         | x        | x    | x      | x      | x    | x      | x        | x              | x    | x        | x        | x    | x       | x        |
| label                             | x      | x         | x        | x    | x      | x      | x    | x      | x        |                | x    | x        | x        | x    | x       |          |
| help_text                         | x      | x         | x        | x    | x      | x      | x    | x      | x        |                | x    | x        | x        | x    | x       |          |
| values                            | x      | x         | x        |      | x      | x      |      |        |          |                |      |          |          |      |         |          |
| icons                             | x      |           |          |      |        |        |      |        |          |                |      |          |          |      |         |          |
| widget                            | x      |           |          |      |        |        |      |        |          |                |      |          |          |      |         |          |
| join_with                         |        | x         |          |      |        |        |      |        |          |                |      |          |          |      |         |          |
| default_value                     | x      | x         | x        |      | x      | x      |      | x      | x        |                | x    | x        | x        | x    | x       |          |
| markup                            |        |           |          | x    |        |        |      |        |          |                |      |          |          |      |         |          |
| ajax                              | x      |           |          |      | x      |        |      |        |          |                |      |          |          |      |         |          |
| multiple                          |        |           |          |      |        |        | x    |        |          |                |      |          |          |      |         |          |
| accept                            |        |           |          |      |        |        | x    |        |          |                |      |          |          |      |         |          |
| restrict_values_from_other_field  |        |           |          |      | x      |        |      |        |          |                |      |          |          |      |         |          |
| restrict_values_from_radios_field | x      |           |          |      | x      |        |      |        |          |                |      |          |          |      |         |          |
| pattern                           |        |           |          |      |        |        |      |        | x        |                | x    | x        |          |      | x       |          |
| pattern_hint                      |        |           |          |      |        |        |      |        | x        |                | x    | x        |          |      | x       |          |
| pattern_browser_only              |        |           |          |      |        |        |      |        | x        |                | x    | x        |          |      | x       |          |
| pattern_by_field_name             |        |           |          |      |        |        |      |        | x        |                | x    | x        |          |      | x       |          |
| pattern_by_field_pattern          |        |           |          |      |        |        |      |        | x        |                | x    | x        |          |      | x       |          |
| pattern_by_field_hint_suffix      |        |           |          |      |        |        |      |        | x        |                | x    | x        |          |      | x       |          |
| not_submittable                   | x      | x         | x        |      | x      | x      | x    | x      | x        |                | x    | x        | x        | x    | x       |          |
| ref                               |        |           |          |      |        |        |      |        |          | x              |      |          |          |      |         |          |
| fields                            |        |           |          |      |        |        |      |        |          | x              |      |          |          |      |         | x        |
| mask                              |        |           |          |      |        |        |      | ?      | x        |                | x    | x        | ?        |      |         |          |
| telprefix_prefix_by_field         |        |           |          |      |        |        |      |        |          |                |      | x        |          |      |         |          |
| validation                        | x      | x         | x        |      | x      | x      | x    | x      | x        |                | x    | x        | x        | x    | x       |          |
| min                               |        |           |          |      |        |        |      | x      |          |                |      |          |          | x    |         |          |
| max                               |        |           |          |      |        |        |      | x      |          |                |      |          |          |      |         |          |
| step                              |        |           |          |      |        |        |      | x      |          |                |      |          |          |      |         |          |
| placeholder                       |        |           |          |      |        |        |      |        |          |                |      |          |          |      | x       |          |
| autocomplete_route_name           |        |           |          |      |        |        |      |        | x        |                |      |          |          |      |         |          |
| submit_format                     |        |           |          |      |        |        |      |        |          |                |      |          |          |      | x       |          |
| grouping_field                    |        |           |          |      |        |        |      |        |          |                |      |          |          |      |         | x        |
| label_change                      | x      |           |          |      | x      |        |      |        |          |                |      |          |          |      |         | x        |
| maxlength                         |        |           |          |      |        |        |      |        | x        |                |      |          | x        |      |         |          |
| minlength                         |        |           |          |      |        |        |      |        | x        |                |      |          | x        |      |         |          |
| form_element_additional_id        |        |           |          |      |        |        |      |        | x        |                | x    | x        |          |      | x       |          |
| check_all_fields                  |        |           | x        |      |        |        |      |        |          |                |      |          |          |      |         |          |

#### id
**Description:**
Unique id of the file. Has to match object name and field api name provided with camelCase eg. `companyDetailsCompanyEmail` where `companyDetails` is an object and `CompanyEmail` is the name of an API field. In case of non submittable fields (see submittable and not subbmitable section) ID might be anything, but should be provided with camelCase.

**Required:**
yes

**Examples:**
```
id: companyDetailsCompanyEmail
```


#### api_name
**Description:**
Name of the field provided with Salesforce API. `api_name` key has to always be defined and it needs to be filled up for the API submittable fields, for non submittable fields this key must be defined and it has to be empty.

**Required:**
yes

**Examples:**
```
# Submittable example
api_name: paymentTermType

# Non submittable example:
api_name:
```


#### api_object
**Description:**
Name of the object field is assign to provided by Salesforce API. `api_object` key has to always be defined and it needs to be filled up for the API submittable fields, for non submittable fields this key must be defined and it has to be empty.

**Required:**
yes

**Examples:**
```
# Submittable example
api_object: orderCase

# Non submittable example:
api_name:
```


#### label
**Description:**
English, translatable version of label for the field which is going to be displayed on the form.

There is one case when this property is required - it has to be always defined when there are connector type fields on the form combined with the initial field. So for initial field label is required.

**Required:**
no

**Examples:**
```
label: `Payment term type`
```


#### help_text
**Description:**
English, translatable version help text which is going to be displayed as a drupal form field description.

**Required:**
no

**Examples:**
```
help_text: `Please enter the first 6 and last 4 digits of your card number.`
```


#### values
**Description:**
Values for fields which supports multiple values. Should be defined as key / value entry for a single value. Each key / value should be defined in a separate line.

**Required:**
no

**Examples:**
```
values:
  'GLN': 'GLN'
  'EHF': 'E-mail'
  'E-Invoice': 'EDI'
```


#### icons
**Description:**
List of key / value icons which will be displayed instead of radio buttons. Key must match the value within values property, value must be an ID of a SLIM service icon. Number of key / value lines must be the same as number of entries defined in values property. This property required a `widget: icons` property. See widget property for details.

**Required:**
no, but requires `widget` property to be defined.

**Examples:**
```
icons:
  new_order: 177
  new_delivery_address: 64
  new_tank: 190
```


#### widget
**Description:**
A form field widget type. So far this property supports only one widget type, which is `icons`. This property must be defined, if `icons` property is used.

**Required:**
no, but requires `icons` property to be defined.

**Examples:**
```
widget: icons
```


#### join_with
**Description:**
A property which allows to gather multiple form values into a single one. This one is supported by `connector` type field only. For example, a `description` field (which is the SF API field) expects to contain multiple values with labels separated by a `;` character.  So eventually the part of payload of description field looks like this:

```
Additional information: some extra info; Another info: some wise content; Product: name_of_the_product;
```

So to gather all the required data and send it as single field value to API (let
's assume it'd be `description` field which should gather all the data) you have to use `connector` type field with `join_with` property. A single `connector` type field represents a single value which is going to be merged to desired field (in case of this example `description` field). If you want more fields to be merged to a `description` value then more connectors you have to define.

Properties of `join_with`:
 - `field_details` - details of the initial field to combine with. This has to include `id`, `api_name`, `api_object`. In case of our example it'd be `orderCaseDescription` field.
 - `separator` - by default it's set to `;` but you can define your own
 - `submit_label` - a label which is going to be used in value of description ready to send to API
 - `render_as` - by default this field is rendered as textarea, but you can define different form element, like select. If select is provided then the definition of a field has to contain `values` property.
**Required:**
no, but required if `connector` field type is used

**Examples:**
```
# Example below will join a connector field with description field. Field is going to be rendered as select field. The value passed to description field is going to be: Agrol User: some_value.

join_with:
  field_details:
    id: orderCaseDescription
    api_name: description
    api_object: orderCase
  separator: ';'
  render_as: select
  submit_label: 'Agrol User'
```


#### default_value
**Description:**
to update

**Required:**
no

**Examples:**
```
default_value: invoice_number
```


#### markup
**Description:**
Text is going to appear in item type field.

**Required:**
no

**Examples:**
```
markup: 'Product fields'
```


#### ajax
**Description:**
Applicable for radios and select field types only. Definition of this property required to define:
 - `method` - for example `defineNumberOfFieldInstances`. This is a PHP public method and needs to be part of `Drupal\ck_salesforce\FormGenerator` class.
 - `wrapper` - an ID of a wrapper in which fields are going to be grouped, eg. `card-instances-wrapper`
 - `fields` - list of fields to process. In case of `defineNumberOfFieldInstances` method this duplicates sets of defined fields. All groups of fields are wrapped with html element of ID defined in `wrapper`, for example: `<div id="card-instances-wrapper">here comes groups of duplicated fields</div>`

This property has very wide functionality. So far there is only one method defined for duplicating groups of fields, but this might be anything. For current usage we have a select (or radios on Ingo Application form) field on Card App for Govern form. Based on how many elements are selected in the field same number of field groups listed in `fields` property are going to be rendered. In our case there's a possibility to order cards and depending on how many cards is selected then corresponding number of field groups are rendered, so user can provide details for each card.

**Required:**
no

**Examples:**
```
ajax:
  method: 'defineNumberOfFieldInstances'
  wrapper: 'card-instances-wrapper'
  fields:
    - caseItemCardCategory
    - caseItemCardType
    - caseItemPurchaseCategory
    - caseItemCardText
    - caseItemMileage
    - caseItemCountryRestricion
```


#### multiple
**Description:**
Multiple is applicable to file field type only. By providing this property and setting to TRUE file upload field is able to collect multiple files at once.

**Required:**
no

**Examples:**
```
multiple: TRUE
```


#### accept
**Description:**
Multiple is applicable to file field type only. By providing this property you can list file extensions this field is allowed to upload. Check [accept](https://developer.mozilla.org/en-US/docs/Web/HTML/Attributes/accept) attribute for more info.

**Required:**
no

**Examples:**
```
accept: 'image/*'
accept: 'image/*,.pdf'
```


#### restrict_values_from_other_field
**Description:**
Allows to restrict field values from another field based on matching criteria defined in a field definition. For example, you want to have two dependent select fields. Let's assume first field has following values: `fruit`, `vegatable`. Second field has following values: `apple`, `pear`, `watermelon`, `carrot`, `potato`, `parsley`. While selecting a `fruit` in the first field it causes second field selection to be narrow down to: `apple`, `pear`, `watermelon`. Similar with the `vegatable` option.

Structure of property:
 - a field key which values should be filtered out
	 - `field_details` - requires defining `id`, `api_name`, `api_object`
	 - `values mapping` - this is the mapping between two fields, each option from the first field defines list of filtered options from second field.

**Required:**
no

**Examples:**
```
restrict_values_from_other_field:
  caseItemPurchaseCategory:
    field_details:
      id: caseItemPurchaseCategory
      api_name: purchaseCategory
      api_object: caseItem
    values_mapping:
      'Fleet':
        - 'A'
        - 'B'
        - 'C'
        - 'D'
        - 'E'
        - 'F'
      'Truck':
        - '60'
        - '61'
        - '62'
        - '63'
        - '64'
        - '65'
      'Europe':
        - '60'
        - '61'
        - '62'
        - '63'
        - '64'
        - '65'
```


#### pattern
**Description:**
A property which allows to define a regex for field validation. See [pattern](https://www.w3schools.com/tags/att_input_pattern.asp) for more info.

Validation will be performed by web browser and later (on submit) by Drupal's FormElement::ValidatePattern().

**Required:**
no

**Examples:**
```
pattern: '^[\d\s\w.,-]{0,27}$'
```


#### pattern_hint
**Description:**
A property which allows to define a message to end user if validation has not passed. This property should be used together with `pattern` property.

**Required:**
no

**Examples:**
```
pattern_hint: 'Max length of 27 characters, no special characters allowed.'
```
#### pattern_browser_only
**Description:**
A property which allows to use pattern attribute only in the web browser (will not be use by Drupal). This property must be used together with `pattern` property.

Drupal's FormElement::ValidatePattern() uses RegExp object as ECMA 262 (JavaScript) variant, web browsers are mainly using PCRE\PCRE2 variant. If PCRE is required then use this property to disable Drupal validation completely.

**Required:**
no

**Examples:**
```
pattern_browser_only: TRUE
```

#### pattern_by_field_name
**Description:**
This property makes possible to dynamically change "pattern" validation of input field based on other field's value.
Example case would be "country selector" and "postal code". Changed value in "country seelctor" cause field "postal code" to change pattern based on selected country.

**Required:**
no

**Examples:**
```
pattern_by_field_name: legal_country_code
```

#### pattern_by_field_pattern
**Description:**
This property must be used together with `pattern_by_field_name` property.
Defines pattern values for each value from field set in `pattern_by_field_name`.

**Required:**
no

**Examples:**
```
pattern_by_field_pattern:
  'DK': '^[\d]{4,4}$'
  'EE': '^[\d]{5,5}$'
```

#### pattern_by_field_hint_suffix
**Description:**
This property must be used together with `pattern_by_field_name` property and is addition to `pattern_hint`.
You can add additional pattern hint info per `pattern_by_field_name` value.

**Required:**
no

**Examples:**
```
pattern_by_field_hint_suffix:
  'DK': 'XXXX (4 digits)'
  'EE': 'XXXXX (5 digits)'
```

#### not_submittable
**Description:**
Boolean value which specifies whether the field should be sent during the submit form.
Define if this field should not send to API when type is hidden.
If not_submittable == TRUE then not send
If not_submittable is not set or not_submittable == FALSE then send

**Required:**
no

**Examples:**
```
not_submittable: TRUE

```

#### ref
**Description:**
Key - value represents information about how to refer this field to created object (from fields). Only for multiple_field field.
Key:value will be added to created object eg contact / address.

**Required:**
no

**Examples:**
```
ref:
  contactRef: cont

# Submitted JSON Object:

orderCase => [
  contactRef => cont0
],
contactPerson => [
  0 => [
    contactFirstName => Carotest,
    contactLastName => Linetest,
    contactPhone => 00000012,
    contactEmail => carotest@linetest.test,
    contactRef => cont0,
  ]
]

```


#### fields
**Description:**
List of fields for multiple_field field. This fields will be displayed in one container.
List of fields for grouping field. This fields will be grouping to one field.

**Required:**
yes for multiple_field and grouping field

**Example:**
```
# For multiple_field
fields:
  delivery_address:
    id: addressStreet
    type: textfield
    label: 'Delivery Street Name'
    help_text:
    api_name: street
    api_object: address
  delivery_city:
    id: addressCity
    type: textfield
    label: 'Delivery City'
    help_text:
    api_name: city
    api_object: address
  delivery_country_code:
    id: addressCountry
    type: country
    label: 'Delivery Country Code'
    help_text:
    api_name: country
    api_object: address
  delivery_postal_code:
    id: addressPostalCode
    type: textfield
    label: 'Delivery Postal Code'
    help_text:
    api_name: postalCode
    api_object: address

# For grouping field
fields:
  -
    id: orderCaseDescription
    api_name: description
    api_object: orderCase
  -
    id: secondOrderProduct
    api_name: null
    api_object: null
```


#### mask
**Description:**
String describes format of data required in this field. Used library: https://imask.js.org/

**Required:**
no

**Example:**
```
mask: '000000{ ⁕⁕⁕⁕⁕⁕ }0000'
```

#### telprefix_prefix_by_field
**Description:**
This property makes possible to dynamically change "prefix" input value based on other field's value.
Example case is "country selector" or any other field having values as contry codes - NO, SE, DK etc. Changed value in "country selector" causes prefix value to be set as given country telephone international prefix.

**Required:**
no

**Examples:**
```
telprefix_prefix_by_field: legal_country_code
```

#### validation
**Description:**
List of validation methods. Key - name of method (existing in ck_salesforce module) to validate data from this field. Value - settings for validation method to compare with field data, eg max number of digits.

**Required:**
no

**Example:**
```
validation:
  digits: 8

validation:
  range:
    min: 17
    max: 18
```


#### min
**Description:**
Number/string represents minimum value using in number/date field.

**Required:**
no

**Example:**
```
# For number field:
min: 0.01

# For date field:
min: 'today'
```

#### max
**Description:**
Number represents minimum value using in number field.

**Required:**
no

**Example:**
```
max: 100
```


#### step
**Description:**
Number represents step for number field.

**Required:**
no

**Example:**
```
step: 0.01
```


#### placeholder
**Description:**
String displayed in time field. Using for datetime fields.

**Required:**
no, but it should be used with submit_format, pattern and pattern_hint

**Example:**
```
placeholder: '00:00'
```

#### autocomplete_route_name
**Description:**
Route name which returns data for autocomplete field. Using for textfield fields. This sets up autocomplete functionality. In our case we are using it for station fields.

**Required:**
no

**Example:**
```
autocomplete_route_name: ck_form.autocomplete.stations
```

#### submit_format
**Description:**
Define datetime submit format. Check available formats: https://php.net/manual/en/function.date.php

**Required:**
no

**Example:**
```
submit_format: 'c'
```

#### grouping_field
**Description:**
Name of the field where grouped data is going to appear.  We use API NAME as this always has to be a field which is part of payload.

**Required:**
yes for grouping type

**Example:**
```
grouping_field: description
```

#### label_change
**Description:**
List of fields with field_details and values_mapping to define new label based on values selected in this field.
**Required:**
no

**Example:**
```
label_change:
  orderCaseBankAccountNumber:
    field_details:
      id: orderCaseBankAccountNumber
      api_name: bankAccountNumber
      api_object: orderCase
    values_mapping:
      local_bank_account: 'Bank Account Number'
      foreign_bank_account: 'IBAN number'
  orderCaseBankRegistrationNumber:
    field_details:
      id: orderCaseBankRegistrationNumber
      api_name: bankRegistrationNumber
      api_object: orderCase
    values_mapping:
      local_bank_account: 'Bank Registration Number'
      foreign_bank_account: 'SWIFT/BIC code'
```

#### maxlength
**Description:**
The maximum string length that the user can enter into an input or textarea. The attribute must have an integer value of 0 or higher.
**Required:**
no

**Example:**
```
maxlength: 10
```

#### minlength
**Description:**
The minimum string length that the user can enter into an input or textarea. The attribute must have an integer value of 0 or higher.
**Required:**
no

**Example:**
```
minlength: 10
```

#### form_element_additional_id
**Description:**
The more complicated form gets the more element name (id) collision is likely to happen. If necessary use this as an extra "description" of an element in generated form. It can be used as 'delta' parameter.
Usage implemented in pattern_by_field_pattern functionality.

**Required:**
no

**Examples:**
```
form_element_additional_id : someAddtionalIdForElementInForm
```

#### check_all_fields
**Description:**
This property is used for checkbox field type. It allows to check all fields in the form, defined in the list. 

**Required:**
no

**Examples:**
```
check_all_fields:
  - mktConsentEmail
  - mktConsentPhone
  - mktConsentSMS
```
