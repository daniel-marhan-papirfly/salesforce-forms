# Submit structure difinition

This file describes the structure sent to the SF API for each endpoint. On the first level are name of endpoints. 
This structure are mapped to JSON object and sent to SF API. Keys are object names (eg company / address / customerType). 
If in value is NULL it means that we expect simple value there (eg string). If in value is [] it means that we expect more complex structure there (eg array, list of objects, list of fields)

### Example

```
genericCase:
  customer:
    customerType: NULL
    businessUnit: NULL
    topic: NULL
    company: []
    contactPerson: []
    deliveryContactPerson: []
    address: []
    orderCase:
      caseItem: []
    tank: []
    attachment: []
cardApplicationCase:
  customer:
    customerType: NULL
    businessUnit: NULL
    topic: NULL
    company:
      contactPerson: []
    address: []
    orderCase:
      caseItem: []
    attachment: []

```
